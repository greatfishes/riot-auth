```python
import requests
import urllib.parse

try:
    response = requests.post('https://riot-auth.vercel.app/login_url')
    response.raise_for_status()
    response = response.json()
    
    login_url = urllib.parse.quote(response.get('login_url'))
    print('To authenticate, scan the QR code below with your mobile device.')
    print(f'https://api.qrserver.com/v1/create-qr-code/?size=512x512&data={login_url}')
    

    input('\nAfter authentication, press Enter.')
    
    token_response = requests.post('https://riot-auth.vercel.app/get_token')
    token_response.raise_for_status()
    token_data = token_response.json()
    
    print('\nResponse data:')
    print(token_data)
    
except requests.exceptions.RequestException as e:
    print('Error:', e)
```
