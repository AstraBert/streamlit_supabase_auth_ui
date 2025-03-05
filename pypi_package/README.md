<div align="center">
<h1>streamlit_supabase_auth_ui</h1>
<h2>Seamless Supabase authentication for seamless Streamlit apps</h2>
</div>
<br>
<div align="center">
    <img src="https://img.shields.io/github/commit-activity/t/AstraBert/streamlit_supabase_auth_ui" alt="GitHub commit activity">
    <img src="https://img.shields.io/pypi/pyversions/streamlit_supabase_auth_ui" alt="Static Badge">
    <img src="https://static.pepy.tech/badge/streamlit-supabase-auth-ui" alt="PyPI Downloads">
    <img src="https://img.shields.io/badge/Release-v0.0.1.post4-blue" alt="Static Badge">
    <br>
    <br>
    <img src="./imgs/supabase_logo.png" alt="Supabase Logo" width="100" style="margin-right: 10px;">
    <img src="./imgs/plus.jpg" alt="plus" width="30" style="margin-right: 10px;">
    <img src="./imgs/streamlit_logo.jpg" alt="Streamlit Logo" width="100">
</div>


### Purpose and Inspiration

[**Streamlit**](https://streamlit.io/) is a popular backend-to-frontend app development framework for python, and over the years several solutions have been developed to tackle user authentication and management for Streamlit apps.

The most popular of them, [streamlit-authenticator](https://github.com/mkhorasani/Streamlit-Authenticator)and [streamlit_login_auth_ui](https://github.com/GauriSP10/streamlit_login_auth_ui), although offering several advanced functionalities and dynamic UIs, lack a reliable backend, database-centered user management (which is generally performed through local files).

We decided to build a new authentication UI, based on [Gauri Prabhakar](https://github.com/GauriSP10)'s login interface, that combines the power of [**Supabase**](https://supabase.co)PostgreSQL databases with the seamless frontend components from **Streamlit**, connecting it also to the e-mail notifications service offered by [**Courier**](https://www.courier.com/) .

The UI has login, user registration, password reset and 'forgot password' functionalities, as well as a logout one.

So, let's get started!🚀

### Third party services

#### 1. Supabase

We will need a Supabase account to build a project, retrieve its URL and ANON key and create a `user_authentication` database, that will connect our UI to the backend, database-centered user-management.

In order to do that, we:

1. Create a [Supabase account](https://supabase.com/dashboard/sign-up)
2. Go to [our dashboard](https://supabase.com/dashboard/projects)
3. Create a new project
4. Go to `Project Settings > API` and copy `URL` under `Project URL` and `anon public` key under `Project API Keys`
5. Copy the URL to `supa_url` and the ANON key to `supa_key` in [`.streamlit/secrets.toml`](./.streamlit/secrets.toml)
6. Open SQL editor on Supabase and execute the following command:
```sql
CREATE TABLE user_authentication (
    id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    username VARCHAR(255) DEFAULT NULL,
    password VARCHAR(255) DEFAULT NULL,
    email VARCHAR(255) DEFAULT NULL,
    name VARCHAR(255) DEFAULT NULL,
    created_at TIMESTAMP DEFAULT NOW(),
    last_login FLOAT DEFAULT 0,
    last_logout FLOAT DEFAULT 0
);
```

#### 2. Courier

We want to send email notifications basically for two reasons:

- Welcome our new users upon registration 
- Send them reset passwords when they want to change their old/lost password

To do so, we use the already mentioned Courier, and so we need to:

1. [Sign up](https://app.courier.com/signup) to Courier
2. Create a new workspace
3. Enable an e-mail service provider. The easiest and cheapest choice is **Gmail**: you only need to specify the Gmail account for which you want to activate the service, which will also be one that will send all the emails.
4. Retrieve the **authorization token** from `Settings > API Keys` 
5. Copy the authorization token and place it under `courier_auth_token` in [.streamlit/secrets.toml](./.streamlit/secrets.toml) 

### Create your application

#### 1. Build from source

We now want to create our Streamlit application with Supabase authentication and user management, and, in order to do so, we:

1. Clone this repository and go inside it:
```bash
git clone https://github.com/AstraBert/streamlit_supabase_auth_ui.git
cd streamlit_supabase_auth_ui
```
2. Create a python virtual environment and activate it:
```bash
python3 -m venv streamlit-app
source streamlit-app/bin/activate
```
3. Install all the required dependencies:
```bash
python3 -m pip install -r requirements.txt
```
4. Modify [`.streamlit/secrets.toml`](./.streamlit/secrets.toml) with the Supabase project URL (`supa_url`), Supabase project ANON key (`supa_key`) and Courier authentication token (`courier_auth_token`) we retrieved beforehand
6. Run the application:
```bash
python3 -m streamlit run app.py
```

You can obviously customize the Streamlit application as much as you want, you will only need to integrate this peace of code to make the Supabase-based auth to work:

```python
import streamlit as st
from .streamlit_supabase_auth_ui.widgets import __login__

__login__obj = __login__(auth_token = st.secrets["courier_auth_token"],
                    company_name = "YOUR-ORG-NAME",
                    width = 200, height = 250,
                    logout_button_name = 'Logout', hide_menu_bool = False,
                    hide_footer_bool = False,
                    lottie_url = 'https://assets2.lottiefiles.com/packages/lf20_jcikwtux.json')

LOGGED_IN= __login__obj.build_login_ui()

if LOGGED_IN == True:

   ### Your Streamlit app here!
```

#### 2. Get PyPi package

We made `streamlit-supabase-auth-ui` also a python package available on PyPi, that you can find [here](https://pypi.org/project/streamlit-supabase-auth-ui/).

To get it, it is sufficient to run:

```bash
python3 -m pip install streamlit-supabase-auth-ui
```

And the installation process will take care of mounting all the necessary dependencies✅

You can then simply import the package in your code:

```python
import streamlit as st
from streamlit_supabase_auth_ui.widgets import __login__

__login__obj = __login__(auth_token = st.secrets["courier_auth_token"],
                    company_name = "YOUR-ORG-NAME",
                    width = 200, height = 250,
                    logout_button_name = 'Logout', hide_menu_bool = False,
                    hide_footer_bool = False,
                    lottie_url = 'https://assets2.lottiefiles.com/packages/lf20_jcikwtux.json')
```

### Live demo

Find a live demo on [HuggingFace Spaces](https://huggingface.co/spaces/as-cle-bert/streamlit-supabase-auth-ui).

### Contributions

Contributions are more than welcome! See [contribution guidelines](./CONTRIBUTING.md) for more information :)

### Funding

If you found this project useful, please consider to [fund it](https://github.com/sponsors/AstraBert) and make it grow: let's support open-source together!😊


### License and rights of usage

This project is provided under [MIT license](./LICENSE): it will always be open-source and free to use.

If you use this project, please cite the author: [Astra Clelia Bertelli](https://astrabert.vercel.app)
