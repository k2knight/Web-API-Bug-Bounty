# Tips from blogs

```
Bug Bounty Tips: 🐛💰 Here's a simple bug bounty tip for shopping site targets that can earn you some serious $$$$.  
  
I've stumbled upon 10+ similar issues on shopping sites that allow guest checkouts 🛒.  
  
Many overlook these issues because they require placing an order 📦. However, some services support cash on delivery 💸 or allow you to place a cheap order and then cancel it for a refund 🔄, making it worth adding to your checklist if other prerequisites are met.  
  
Here's what to look for:  
  
1️⃣ Target app that permits guest orders without creating an account 🕵️‍♂️  
2️⃣ Target app doesn't require email verification for new account creation, or you've found an email verification bypass on sign-up 📧🔓  
  
If these prerequisites are met, you can often find target apps with a misconfiguration that lets you access a guest user's order history by creating a new account with the same email used for the guest order.  
  
Here's how it usually goes down:  
  
1️⃣ Place an order on the site as a "Guest" and use the victim's email during checkout, e.g., [victim@example.com](mailto:victim@example.com) 📩  
2️⃣ The victim receives an email with the receipt 📧  
3️⃣ As an attacker, sign up using the email [victim@example.com](mailto:victim@example.com) assuming there's no email verification 🧑‍💻  
4️⃣ Navigate to the account's order history page, and you might strike gold 🪙 by finding the previously made orders, leading to Order History and PII leaks 🔍📜  
  
🚀 Takeaways: Don't ignore workflows involving payments; you might discover workarounds like cheap payments or cash on delivery 💡💳. Test for unusual flows and be ready for pleasant surprises with some lucrative bounties 💰💎 #BugBounty #CyberSecurity #HackerOne #BugBountyTips #SecurityTips #Bounties #infosecurity
```

```
Bug Bounty Tips: 🐛🔐 Email Verification Bypass Tips  
  
Working on a target where email verification is crucial? Imagine a scenario where gaining access to a specific domain, like example[.]com, could grant you entry into a victim's workspace, allowing you to view documents and other content associated with that whitelisted domain.  
  
Often, email verification bypass issues are reported without demonstrating real-time impact or as pre-account takeovers. Consequently, many of these submissions get marked as "Informative."  
  
Here's my approach on how to showcase the impact of these issues:  
  
Identify Features Dependent on Email Domain:  
Identify critical features linked to a user's email domain. For instance, consider a target app that grants access to resources based on your email domain. Some apps let you join a team or workspace directly if your email matches the team's domain (e.g., join Victim SITE XYZ only with sample@victimsitexyz[.]com). Others restrict access to documents or videos based on email domain whitelisting. Numerous such opportunities exist where email plays a crucial role.  
  
Here's a simple trick that often works to bypass email verification and claim an unregistered email on any domain:  
  
1️⃣ Log in to your attacker account and change your email address to an attacker-controlled email (e.g., [attackeremail@attackerdomain.com](mailto:attackeremail@attackerdomain.com)).  
  
2️⃣ You'll likely receive an email confirmation link on your attacker-controlled email (Do not verify it yet).  
  
3️⃣ Now, change your email to the unregistered email or domain you wish to HIJACK (e.g., [victimemail@victimdomain.com](mailto:victimemail@victimdomain.com)).  
  
4️⃣ This action will send an email verification link to [victimemail@victimdomain.com](mailto:victimemail@victimdomain.com), which you don't have access to.  
  
5️⃣ Try clicking on the "Email" verification link sent earlier to [attackeremail@attackerdomain.com](mailto:attackeremail@attackerdomain.com). If the system fails to revoke the previous email verification link, the link for [attackeremail@attackerdomain.com](mailto:attackeremail@attackerdomain.com) could end up verifying the email for [victimemail@victimdomain.com](mailto:victimemail@victimdomain.com), allowing you to claim it as verified.  
  
Once you've claimed an email associated with another organization's domain, identify the associated functions to prove impact and report it to earn some generous bounties!  
  
Numerous similar misconfigurations exist that you can leverage to bypass email verification checks.  
  
Takeaways: Don't report email verification issues without demonstrating actual impact. Apps that support organizations/workspaces with multiple roles often rely on a person's email domain, making them valid candidates for showcasing security impact. 💡🛡️
```