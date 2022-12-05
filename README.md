### Style transfer web app With Keycloak authentication , NGINX reverse proxy and load balancing.

#### Tools used
- FastAPI: for the API
- streamlit : for the interface
- Docker: to containerize the app
- keycloak for User authentication
- Nginx for load balancing and ssl

#### Download the models
```bash
./download_models.sh
```

#### Place .env file in the project root directory with appropriate values
```bash
DB_VENDOR=MYSQL
DB_ADDR=DB-HOST
DB_DATABASE=DB-NAME
DB_USER=DB-USER
DB_PASSWORD=DB-VALUE
KEYCLOAK_USER=admin
KEYCLOAK_PASSWORD=VALUE
```

#### Place your domains SSL cerficates in certs folder in project root. 
```bash
/certs/fullchain.pem
/certs/privkey.pem
```

#### Change the Keycloak code attributes /frontend/main.py 
```python
st.title("style-transfer")
keycloak = login(
    url="https://your-domain/auth",
    realm="master",
    client_id="your client id",
    auto_refresh=False
)
```

#### Change the server name in nginx config
```bash
/conf/nginx_rp.conf
```

backend instances are loadbalanced by nginx the conf file is present conf folder
```bash
/conf/backend-lb.conf
```

#### Run
```bash
docker-compose up -d --scale backend=2
```
