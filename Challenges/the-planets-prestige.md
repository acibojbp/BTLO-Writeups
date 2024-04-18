# The Planet's Prestige

### Scenario

CoCanDa, a planet known as 'The Heaven of the Universe' has been having a bad year. A series of riots have taken place across the planet due to the frequent abduction of citizens, known as CoCanDians, by a mysterious force. CoCanDa’s Planetary President arranged a war-room with the best brains and military leaders to work on a solution. After the meeting concluded the President was informed his daughter had disappeared. CoCanDa agents spread across multiple planets were working day and night to locate her. Two days later and there’s no update on the situation, no demand for ransom, not even a single clue regarding the whereabouts of the missing people. On the third day a CoCanDa representative, an Army Major on Earth, received an email.

### Disclaimer

_The information presented here is for educational purposes only. It is crucial to handle phishing incidents with caution and adhere to company policies and cybersecurity best practices._

_All information presented in this repository is sourced from the respective course's materials._

## Solution

Here, we will analyze the email received by the Army Major on Earth in hopes of finding clues about the whereabouts of the missing people. At the end of the challenge, we should be able to answer all the questions. To begin, we must first download the .eml file.

Once we've downloaded the zip and obtained the password provided in the challenge instructions, we'll extract the zip file. Inside, we'll find "A Hope for CoCanDa.eml," which we'll open with Notepad++.

Right from the start, it's evident from the headers that this email raises suspicion. Our reasons for this include:

1. **Mismatched Domains:** The email is purportedly sent from "Bill" `billjobs@microapple.com`, yet it's received from a server with a different domain (`emkei.cz`, IP address `93.99.104.210`). This inconsistency raises suspicion as it's unusual for legitimate emails to be sent from one domain but received from another.
2. **SPF Failure:** The SPF check for the sender's domain, microapple.com, failed. SPF is a mechanism used to prevent email spoofing, so a failed SPF check could indicate that the email was not sent from an authorized server.
3. **Reply-To Address:** The email specifies an alternate email address for replies `negeja3921@pashter.com`. While this is not necessarily indicative of phishing on its own, it's a tactic often used by phishers to divert responses to a different email address.

![01](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/e84590fc-bb17-4aa4-af3a-93f1953b5512)

### **What is the email service used by the malicious actor?**

To determine the email service used by the sender, examine the email headers, particularly focusing on the `Received` headers. These headers document the route the email took from its origin to its final destination.

The `Received` header at the bottom of the email headers is typically the most relevant, as it indicates the initial point of receipt. This bottommost header represents the first point in the email's journey.

In the provided email headers, the first `Received` header indicates that the email originated from a server identified as `emkei.cz` with the IP address `93.99.104.210`. This information suggests that the email was sent using the services provided by `emkei.cz`.

`Emkei.cz` is a website offering various email-related services. Among these services are email spoofing, email testing, and email tracking. One notable feature of `emkei.cz` is its capability to allow users to send emails from any email address without requiring authentication. This feature effectively enables email spoofing, where senders can falsify the sender address to appear as if the email came from someone else.

Ans: `Emkei.cz`

---

### **What is the Reply-To email address?**
  
The `Reply-To` email address specified in the email headers is `negeja3921@pashter.com`

This information can be found in the `Reply-To` header of the email.

In the context of phishing emails, the `Reply-To` header serves as a deceptive element, allowing phishers to specify an alternate email address under their control. 

Recipients should exercise caution when replying to emails, especially from unknown sources, and verify the legitimacy of both the sender's email address and any provided `Reply-To` addresses to avoid falling victim to phishing scams.

Ans: `negeja3921@pashter.com`

---

![02](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/d16c6032-9814-4947-b21f-ed1aeb2a4f1e)

Continuing our investigation, the email body appears to be a multipart MIME message, denoted by the boundary marker "--BOUND_600FB98E0DCEE8.49207210" that separates its various parts. Each boundary marker indicates the type and encoding of the respective parts.

The initial part suggests that it contains plain text encoded in base64. This encoded content likely contains a message or information. To interpret the content, it must first be decoded from base64 encoding.

Upon decoding the first part, we are presented with the following message:

![03](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/03e1924e-3b66-4f18-a74a-dacfe2a8778e)

---

### **What is the filetype of the received attachment which helped to continue the investigation?**

In the next step of our investigation, I took a closer look at the attachment named "PuzzleToCoCanDa.pdf." It was supposed to be a PDF file encoded in base64. But, to be sure about its actual file type, I decided to double-check it.

I copied the entire base64 content of the attachment and converted it into its hexadecimal representation. This conversion allowed for a closer examination of the file's signature.

![04](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/63bf7e96-332c-401a-86ea-f76274702bc6)

By analyzing the first four bytes of the hexadecimal representation, which were `50 4b 03 04,` I cross-referenced this sequence with file signature databases, such as garykessler.net. The information revealed that `50 4b 03 04` corresponds to the signature of a ZIP file, not a PDF. A PDF file typically begins with the file signature `25 50 44 46`.

![05](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/3e64bf30-ae78-4111-8d7d-f9cca3e2bf14)

So, after going through all that, turns out the attachment wasn't a PDF as it was labeled. It's actually a ZIP file. This changes things up a bit in terms of how we handle it. Next steps involve decoding the content from base64 and treating it like the ZIP file it is for extraction and further digging.

![06](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/7656e235-4af6-4a32-894c-2486ce685e02)

Ans: `.zip`

---

After extracting the file, we'll want to make sure that file extensions are visible and hidden items are shown. Once we've done that, we'll be able to see that there are three files present.

![07](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/cec78947-dafc-44c9-b4e2-896b7764b979)

- DaughtersCrown
- GoodJobMajor
- Money.xlsx

To definitively determine the file types, I'll employ HxD to swiftly examine their hex values and analyze the first four bytes.

![08](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/5382e60c-205f-4cc7-8600-67872e827160)

![Uploading 09.png…]()

The first file, DaughtersCrown, has a file signature of `FF D8 FF E0`, indicating a JPG format. Adding a .jpg extension to the file converts it to an image, revealing that it is indeed a crown.

![10](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/9071ef30-8918-4c3b-a636-e255f972e410)

Upon inspecting the next file, GoodJobMajor, I observed that the first four bytes are `25 50 44 46`, a signature familiar to us as we've encountered it before. Upon double-checking, it's confirmed as the file signature of a PDF. Consequently, appending the .pdf extension should convert it into a PDF file, allowing us to open it and search for any pertinent information or clues.

![11](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/95f16b07-3ebe-4c46-b479-2881e924f3f6)

![12](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/8864b262-caa5-47e3-b530-dfdf67799dc3)

> In line with the scenario, the contents of the PDF reveal that the proof is the crown, indicating that the perpetrators indeed possess the princess and are demanding ransom. This ransom information is detailed in the Money.xlsx file.

![13](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/a83cc64c-2bed-4c65-a92f-98f350774950)

Since we've disabled hidden items, allowing us to spot Money.xlsx. To confirm its format, I checked the hex bytes, which indeed confirm that it's an xlsx file.

![14](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/eb685edd-d32c-499a-8360-d1e9ca1b175e)

![15](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/4b4444af-a1b8-480f-921a-e95810a3fadd)

Unfortunately, since I'm conducting this investigation in a virtual lab without access to Microsoft Office, I won't be able to open the xlsx file conventionally. However, I'll use [SquareX: Be Fearless Online (sqrx.com)](https://sqrx.com/), a platform offering a disposable file viewer. This tool will enable me to safely view the xlsx file and proceed with our examination.

![16](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/a3f068d5-97e0-4a74-9fc7-70ce47767115)

Upon opening the xlsx file, we discover two sheets: Sheet 1 and Sheet 3. Sheet 1 contains a message from the attacker, indicating that they will be remaining in the same location.

What's particularly intriguing is the absence of Sheet 2, and Sheet 3 appears to be blank at first glance.

After checking for any hidden sheets without success, I opted to remove any formatting applied to the spreadsheet by right-clicking and selecting "Clear" > "Format." This way, any texts with white font color would become visible if present.

![17](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/fd4a8617-fa4f-4e94-aee6-dd73bacc435d)

And there it was! A base64 encoded message surfaced in Sheet 3 once the formatting was removed.

Plugging this into CyberChef, we unveil another message: `The Martian Colony, Beside Interplanetary Spaceport`

![18](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/8545b737-6063-42c7-8a7e-3a904d4c1706)

This likely serves as the answer to the question, "What is the location of the attacker in this Universe?"

Ans: `The Martian Colony, Beside Interplanetary Spaceport`

---

**What is the name of the malicious actor?**

The sender's email address is "billjobs@microapple.com." However, it's crucial to remember that email addresses can be spoofed or altered. 

While the "Reply-To" email address, "negeja3921@pashter.com," could provide a clue about the sender's identity, it's important to remain cautious as email addresses can be easily manipulated.

Therefore, we can't definitively identify the name of the malicious actor solely based on these information.

With that, I will be examining the metadata of the attachment using a tool called ExifTool, which can be downloaded here : [ExifTool by Phil Harvey](https://exiftool.org/index.html)

![19](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/dbc2d364-b77e-45ec-8750-31b981c4885e)

Based on the metadata pulled via PowerShell, it seems the author is "Pestero Negeja." Given the close match with the "Reply-To" email address, `negeja3921@pashter.com`, it's quite likely that `Pestero Negeja` is our malicious actor's name.

![20](https://github.com/acibojbp/BTLO-Writeups/assets/164168280/ce5fd6d0-3104-4e86-bcf5-44f9a8a3c0dd)

Ans: `Pestero Negeja`

---

**What could be the probable C&C domain to control the attacker’s autonomous bots?****

Based on the email headers, we've identified the `Reply-To` email address as tied to our malicious actor. With this information, we can infer that `pashter.com` is likely the domain used by the malicious actor to control their bots.

Ans: `pashter.com`




