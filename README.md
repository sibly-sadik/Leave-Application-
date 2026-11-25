# Employee Leave Application Form

A clean, corporate leave application form for office use. It is a single HTML file with no build step. Open it in a browser to fill in, print, save as PDF, or send the application over WhatsApp or SMS.

**Stack:** HTML5, [Tailwind CSS](https://tailwindcss.com) (CDN), Vanilla JavaScript, [Lucide](https://lucide.dev) icons, Inter font (Google Fonts).

## Quick start

1. Keep `leave-application-form.html` anywhere on your computer.
2. Double-click it to open in Chrome, Edge, Firefox or Safari.
3. Fill in the form, then use **Submit application** or **Print / Save as PDF**.

An internet connection is required the first time because Tailwind, Lucide and the Inter font load from CDNs. The company logo is embedded in the file, so no image file is needed.

## Features

- **Header:** logo, editable company name (click to edit), auto-generated Reference ID (`LV-YYYYMMDD-####`) and application date. Both can be changed by hand.
- **Employee information:** name, employee ID, designation, department, official email, contact number.
- **Leave details:**
  - Leave type cards: Casual, Sick, Annual/Earned, Emergency, Unpaid (LWP), Maternity/Paternity.
  - Duration: Full day or Half day (first half / second half).
  - Start and end date pickers.
  - **Total leave days** calculated automatically. Half day subtracts 0.5, an optional "Exclude weekends" box skips Saturday and Sunday, and the number can be edited manually (press **Auto** to recalculate).
  - Reason for leave.
- **Work handover and emergency contact:** reliever name and designation, emergency number, address during leave.
- **Declaration and approvals:** declaration checkbox, plus signature and date boxes for the applicant, line manager (Approved / Rejected + remarks) and HR.
- **Validation:** required fields, email and phone format, end date not before start date, positive day count, and declaration. Errors are highlighted and the page scrolls to the first one.
- **Reset form:** clears everything after a confirmation prompt.

## Submit: send via WhatsApp or SMS

When the form is valid, **Submit application**:

1. Builds a text summary of the application.
2. Opens WhatsApp (`wa.me`) with that message addressed to the receiver number.
3. Shows a modal with the summary and fallback buttons: **Open WhatsApp again**, **Send as SMS instead**, **Print copy**.

> **Important:** a plain HTML file cannot send a message silently. The browser only opens WhatsApp or the SMS app with the message ready, and the user must press **Send**. To send without that step, you need a backend or an SMS/WhatsApp API (for example Twilio).

"Send as SMS" works on phones. Desktop computers usually have no SMS app, so use WhatsApp there.

### Change the receiver number

In the `<script>` section, edit this line (country code first, no `+` or spaces):

```js
const RECEIVER = '8801824381816';   // +880 1824-381816
```

## Print / Save as PDF (one A4 page)

Click **Print / Save as PDF**. Just before printing, a script measures the form using the print styles and scales it to fit one A4 page (8 mm margins). Buttons, hints and the weekend checkbox are hidden in print.

In the print dialog, use:

| Setting | Value |
| --- | --- |
| Destination | Save as PDF |
| Paper size | A4 |
| Margins | Default |
| Headers and footers | Off |
| Background graphics | On |

Chrome and Edge give the most reliable result. The page scaling uses the CSS `zoom` property, so very old browsers may print on two pages.

## Customization

| What | Where |
| --- | --- |
| Company name | Click it in the header, or change the text inside `<h1 id="companyName">` |
| Logo | Replace the `src="data:image/png;base64,..."` on the header `<img>`, or point it at a file such as `src="logo.png"` |
| Accent color | Replace `indigo-*` Tailwind classes (for example `indigo-600`) with another color |
| Departments | Edit the `<option>` list in the `#department` select |
| Leave types | Edit the `LEAVE_TYPES` array in the script (`[name, lucide-icon-name]`) |
| Receiver number | `RECEIVER` constant in the script |
| Print scale limits | `fitPrint()` function (`725` = usable width, `1035` = usable height, in px) |

## File structure

```
leave-application-form.html   The whole app (HTML + CSS + JS + embedded logo)
README.md                     This file
```

## Notes

- Nothing is stored. All data stays in the browser tab and is lost on refresh unless it is printed or sent.
- The form does not upload data to any server. The only outgoing action is opening WhatsApp or SMS with the message text.
- Signature boxes are blank for handwritten signatures after printing.

## Browser support

Latest Chrome, Edge, Firefox and Safari. Mobile browsers work for filling in and sending; use a desktop browser for the best PDF output.
