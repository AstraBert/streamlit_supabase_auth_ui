<div align="center">
<h1>streamlit_supabase_auth_ui</h1>
<h2>Seamless Supabase authentication for seamless Streamlit apps</h2>
</div>
<br>
<div align="center">
    <img src="imgs/supabase_logo.png" alt="Supabase Logo" width="100" style="margin-right: 10px;">
    <img src="imgs/plus.jpg" alt="plus" width="30" style="margin-right: 10px;">
    <img src="imgs/streamlit_logo.jpg" alt="Streamlit Logo" width="100">
</div>

Based on [this original repo](https://github.com/GauriSP10/streamlit_login_auth_ui)

### Full documentation coming soon!

### In the meantime...

1. Create a [Supabase account](https://supabase.com/dashboard/sign-up)
2. Go to [your dashboard](https://supabase.com/dashboard/projects)
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
    created_at TIMESTAMP DEFAULT NOW()
);
```
7. Clone this repo:
```bash
git clone https://github.com/AstraBert/streamlit_supabase_auth_ui.git
cd streamlit_supabase_auth_ui
```
8. Create a virtual env and activate it
```bash
python3 -m venv streamlit-app
source streamlit-app/bin/activate
```
9. Install all the required packages:
```bash
python3 -m pip install -r requirements.txt
```
10. Run the application:
```bash
python3 -m streamlit run app.py
```