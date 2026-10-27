#  Credential-Harvesting-Simulation

Independent Cybersecurity R&D Lab - Web Authentication & Adversary-in-the-Middle (AiTM) Mechanics.

Credential Harvesting & Redirection (R&D Lab)

##  🎯 Project Overview

This project is a custom-built, independent lab environment designed to simulate a credential harvesting workflow. The primary objective was to understand how threat actors intercept HTTP POST requests, locally log sensitive parameters, and execute seamless server-side redirections (bouncing the user to an authentic portal) to avoid detection.

##  🛠️ Lab Architecture

Target OS: Ubuntu 24.04 Virtual Machine (Local IP: 10.61.0.251).

Web Stack: Apache2 and PHP.

Frontend (index.php): An HTML phishing lure utilizing a modified <form> tag designed to route submissions to the local backend rather than the authentic identity provider.

Backend (login.php): A custom PHP request handler.

##  ⚔️ The Attack Vector & System Logic

The simulation relies on three core mechanics:

Capture: The frontend form uses method="POST" to send the victim's inputted UserName and Password to the local login.php script.

Log: The backend intercepts the $_POST array and uses PHP's file_put_contents() to secretly write the credentials and the victim's IP address to a hidden local file (credentials.txt).

Redirect: Immediately after logging the data, the backend executes an HTTP 302 Redirect (header("Location: https://canvas.fontys.nl");), seamlessly pushing the victim to the real authentication portal so they do not realize their initial session was intercepted.

##  🚧 Environmental Challenges & Security Defense Analysis

During the prototyping phase, a perfect visual clone of the target enterprise portal could not be achieved. This lab practically demonstrated the effectiveness of modern defensive web architecture:

CORS & CSP: The target identity provider utilizes strict Cross-Origin Resource Sharing (CORS) and Content Security Policies. Because the local VM (10.61.0.251) was an unauthorized domain, the target server actively blocked the browser from fetching the required CSS stylesheets.

Dynamic Asset Pipelines: The target infrastructure relies on dynamic Content Delivery Networks (CDNs) and JavaScript rendering, proving why advanced threat actors must rely on dynamic reverse proxies (like Evilginx) rather than static HTML clones.

##  📸 Proof of Concept (PoC)
<img width="1158" height="737" alt="Screenshot 2026-10-17 190323" src="https://github.com/user-attachments/assets/0d37ff94-6c18-4dee-b1cf-bf6d2b4a8f01" />
<img width="1212" height="840" alt="Screenshot 2026-10-17 200431" src="https://github.com/user-attachments/assets/3bb1a952-0a7b-499e-8540-02daa9ceb2a7" />
<img width="1108" height="275" alt="Screenshot 2026-10-20 112724" src="https://github.com/user-attachments/assets/bad0c61f-00e6-4070-95bc-f8d9f1de543e" />

