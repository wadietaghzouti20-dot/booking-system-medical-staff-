# RENDEVO Medical Staff Booking

A French-language, mobile-friendly appointment booking site for medical practices and care teams. This is a separate copy of the RENDEVO booking flow, adapted for general medical consultations, follow-up, nursing care, and other medical acts.

## Repository

https://github.com/wadietaghzouti20-dot/booking-system-medical-staff-

## Website

After enabling GitHub Pages from **Settings → Pages → Deploy from a branch → main → /(root)**, the site will be:
https://${owner}.github.io/booking-system-medical-staff-/

## Features in the code

- Multi-step, mobile-friendly patient booking form with validation and consent.
- Live availability from Google Apps Script and conflict prevention for overlapping appointments.
- Google Sheets storage in a separate spreadsheet created by `setupBookingSystem()`.
- Confirmation email to the patient and notification to the practice/team.
- Google Calendar event creation.
- Reminder trigger scheduled for 24 hours before the appointment (Google may delay trigger execution).
- Secure cancellation link with one-time token; cancellation marks the booking as cancelled, removes the reminder trigger, attempts calendar cleanup, and makes the slot available again.
- Formula-injection protection for patient-entered spreadsheet values.

## Important: setup is not finished until the backend is deployed

The frontend's `config.js` intentionally has an empty `appsScriptUrl`. Do not connect it to the dental system's URL, because that would share its spreadsheet, appointments, calendar and notifications.

1. Create a **new** Google Apps Script project for this medical-staff version.
2. Copy the complete `Code.gs` from this repository into the Apps Script editor and save.
3. Run `setupBookingSystem()` once. Approve the requested Google Sheets, Gmail, Calendar and trigger permissions. Keep the spreadsheet URL shown in the execution log.
4. Deploy → New deployment → Web app; execute as your account and allow access as required for a public booking form. Copy the `/exec` URL.
5. Edit `config.js` and set `appsScriptUrl` to that new `/exec` URL.
6. Deploy GitHub Pages, then test a dummy booking, sheet row, confirmation email, calendar event, reminder trigger, cancellation, and re-opening of the cancelled slot.

The clinic/team can set `OWNER_EMAIL` in `Code.gs` before deployment if notifications should go to a specific inbox. Do not use real patient data until access, consent, and privacy handling have been reviewed. This simple booking form is not an emergency service and should not collect detailed medical records.

## Default schedule

Africa/Algiers time zone. The backend schedule copied from the dental system is Sunday–Thursday 08:00–17:00, Friday closed, Saturday 10:00–16:00. Adjust it in `Code.gs` if the medical team has different hours.
