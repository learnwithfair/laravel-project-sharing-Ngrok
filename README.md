# Laravel API Sharing on Windows Using Herd / PHP and Ngrok (With Firewall Setup)
[![Youtube][youtube-shield]][youtube-url]
[![Facebook][facebook-shield]][facebook-url]
[![Instagram][instagram-shield]][instagram-url]
[![LinkedIn][linkedin-shield]][linkedin-url]

Thanks for visiting my GitHub account!


## Prerequisites

* PHP installed (comes with Herd or standalone)
* Laravel project
* Ngrok installed (`ngrok.exe`)
* Herd optional (used for local development environment)

---

## 1. Project Path

Example:

```
C:\Users\Rahatul\Herd\cristi123400_laravel
```

---

## 2. Start Local PHP Server

Open PowerShell in project root:

```powershell
cd C:\Users\Rahatul\Herd\cristi123400_laravel
php -S 0.0.0.0:8888 -t public
```

Expected output:

```
PHP 8.3.28 Development Server (http://0.0.0.0:8888) started
```

* Leave this terminal open.
* Local API access (LAN only):

```
http://<your-local-ip>:8888/api/...
```

---

## 3. Configure Windows Firewall (LAN Access)

If your teammate is on the same WiFi and cannot access your API, open the port in Windows Firewall:

1. Press `Windows + R`, type:

```
wf.msc
```

and press Enter to open **Windows Defender Firewall with Advanced Security**.

2. Click **Inbound Rules** in the left panel.
3. Click **New Rule** in the right panel.
4. Select **Port**, then click **Next**.
5. Select **TCP**.
6. In the **Specific local ports** field, enter:

```
8888
```

7. Click **Next**.
8. Select **Allow the connection**, then click **Next**.
9. Check all profiles:

* Domain
* Private
* Public

10. Click **Next**.
11. Enter a name for the rule:

```
Laravel PHP Server 8888
```

12. Click **Finish**.

> This allows other devices on the same network to access your Laravel server on port 8888.

---

## 4. Configure Ngrok

### 4a. Sign up and obtain token

1. Go to [https://dashboard.ngrok.com/get-started/setup/windows](https://dashboard.ngrok.com/get-started/setup/windows)
2. Copy your **Authtoken**.

### 4b. Add Authtoken

In PowerShell, run:

```powershell
ngrok authtoken <YOUR_TOKEN>
```

Expected output:

```
Authtoken saved to configuration file
```

---

## 5. Expose Local Server via Ngrok

Run:

```powershell
ngrok http 8888 --host-header="localhost:8888"
```

Expected output:

```
Session Status                online
Forwarding                    https://example.ngrok-free.dev -> http://localhost:8888
Forwarding                    http://example.ngrok-free.dev -> http://localhost:8888
Web Interface                 http://127.0.0.1:4040
```

* **Public URL:** Use the HTTPS URL shown under Forwarding.
* This URL can be accessed by teammates, Postman, or frontend apps anywhere.

---

## 6. Update Laravel APP_URL (Optional)

If the Laravel app generates absolute URLs:

```env
APP_URL=https://example.ngrok-free.dev
php artisan config:clear
```

---

## 7. Share API with Teammates

Example endpoints:

```
https://example.ngrok-free.dev/api/login
https://example.ngrok-free.dev/api/users
```

* Works on any network (LAN or Internet).
* HTTPS enabled.
* No additional firewall changes required for ngrok tunnel.

---

## 8. Monitor Requests (Optional)

Ngrok provides a web interface:

```
http://127.0.0.1:4040
```

* View request logs, headers, body, and status
* Useful for debugging

---

## 9. Stop Servers / Switch Back to Herd

### 9a. Stop PHP Server

In terminal running PHP server:

```
Ctrl + C
```

### 9b. Stop Ngrok

In ngrok terminal:

```
Ctrl + C
```

* Public ngrok URL will stop working.

### 9c. Resume Local Development with Herd

1. Ensure the site is linked:

```powershell
herd link cristi123400_laravel
```

2. Access the site in browser:

```
http://cristi123400_laravel.test
```

* Herd automatically handles the server.
* Use this workflow for normal local development.

---

---

## Quick Command Summary

| Task             | Command                                          |
| ---------------- | ------------------------------------------------ |
| Start PHP server | `php -S 0.0.0.0:8888 -t public`                  |
| Add Ngrok token  | `ngrok authtoken <YOUR_TOKEN>`                   |
| Expose Laravel   | `ngrok http 8888 --host-header="localhost:8888"` |
| Check requests   | `http://127.0.0.1:4040`                          |

---

## Notes

* Always start the PHP server before starting ngrok.
* Keep both terminals open while the API is in use.
* Free ngrok URLs change on each session; for persistent URLs, a paid ngrok plan is required.
* Do not share Herd `.test` domains; use ngrok URLs for external access.
* Ensure your teammate is on the same network if using LAN access (Firewall rule required).

---



## Follow Me

[<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/github.svg' alt='github' height='40'>](https://github.com/learnwithfair) [<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/facebook.svg' alt='facebook' height='40'>](https://www.facebook.com/learnwithfair/) [<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/instagram.svg' alt='instagram' height='40'>](https://www.instagram.com/learnwithfair/) [<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/twitter.svg' alt='twitter' height='40'>](https://www.twiter.com/learnwithfair/) [<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/youtube.svg' alt='YouTube' height='40'>](https://www.youtube.com/@learnwithfair)

 <!-- MARKDOWN LINKS & IMAGES  -->

[youtube-shield]: https://img.shields.io/badge/-Youtube-black.svg?style=flat-square&logo=youtube&color=555&logoColor=white
[youtube-url]: https://youtube.com/@learnwithfair
[facebook-shield]: https://img.shields.io/badge/-Facebook-black.svg?style=flat-square&logo=facebook&color=555&logoColor=white
[facebook-url]: https://facebook.com/learnwithfair
[instagram-shield]: https://img.shields.io/badge/-Instagram-black.svg?style=flat-square&logo=instagram&color=555&logoColor=white
[instagram-url]: https://instagram.com/learnwithfair
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=flat-square&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/company/learnwithfair

#learnwithfair #rahtulrabbi #rahatul-rabbi #learn-with-fair
