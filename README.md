# FocusHacks

A web app that uses your webcam and a machine learning model to notice when you lose focus while studying, then emails you a reminder to get back on track. Built at NewHacks 2021.

<!-- Add a screenshot or demo GIF here, e.g. ![demo](docs/demo.gif) -->

## Features

- Classifies webcam frames in real time as **Focused**, **Not Focused**, or **Violating Privacy**
- Tracks a running focus score and pauses tracking once it runs out
- Sends a reminder email with a motivational message when you've been distracted too long
- Detects when someone points a phone at the screen during a virtual class and emails a warning to both the student and the teacher
- Pause and resume tracking at any time

## How it works

```
Webcam ──▶ TensorFlow.js + Teachable Machine model (browser) ──▶ focus / risk scores
                                                                       │ threshold reached
                                                                       ▼
                                       Express server (/email, /warning) ──▶ Twilio SendGrid ──▶ inbox
```

The model was trained with Google's Teachable Machine and runs entirely in the browser through TensorFlow.js. Each prediction updates a focus score, which drops while you're classified as "Not Focused", and a risk score, which drops on confident "Violating Privacy" predictions. When either reaches zero, the page pauses tracking and calls the Express backend, which sends the appropriate email through Twilio SendGrid.

## Tech stack

- **ML:** TensorFlow.js, Teachable Machine (image model)
- **Frontend:** HTML5, CSS3, Bootstrap 5, JavaScript
- **Backend:** Node.js, Express
- **Email:** Twilio SendGrid

## Results

- Real-time focus classification and email alerts working end to end in the browser
<!-- Add any award or placement from NewHacks 2021 here -->

## Running it locally

1. Clone and install:
   ```bash
   git clone https://github.com/Ibrahimkasiim1/FocusHacks.git
   cd FocusHacks
   npm install
   ```
2. Copy `sendgrid-template.env` to `sendgrid.env` and fill in your SendGrid API key, name, and email addresses. Change the sender in `sendGrid.js` to a sender verified in your SendGrid account.
3. Start the server and open [http://localhost:8080](http://localhost:8080):
   ```bash
   node index.js
   ```

## Team

Built at NewHacks 2021 by:

- [Peter Hui](https://github.com/HSKPeter): ML integration, focus tracking, email service
- [Ibrahim Kasim](https://github.com/Ibrahimkasiim1): HTML template, UI and styling
- [Mustafa Abdulrahman](https://github.com/Mustaballer): UI and loading states, branding

## Citations

[1] Steel, P. (2007). The nature of procrastination: A meta-analytic and theoretical review of quintessential self-regulatory failure. *Psychological Bulletin, 133*(1), 65–94. https://doi.org/10.1037/0033-2909.133.1.65
