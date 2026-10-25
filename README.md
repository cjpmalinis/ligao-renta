# LIGAO RENTA — Charlemaigne Motorcycle Rental
**Tagline: ARKILA NA!**

A responsive web-app starter for motorcycle rentals. Initial motorcycles:
- YAMAHA MIO — Matte Gray
- YAMAHA MIO S — Matte Brown

## Features in this starter
- Separate renter account and owner/admin login screens
- Renter registration and sign-in via Supabase Auth
- Availability calendar backed by the online database
- Date/time booking request with overlap checks
- Initial pricing: ₱369 for up to 12 hours; ₱699 per 24-hour day
- Suggested succeeding-day discounts: 5% on day 2, 7% on day 3, 10% on day 4, 15% from day 5 onward
- Owner-adjustable rates and discounts
- Owner can add/deactivate motorcycles
- Required driver's-license upload (JPG/PNG/PDF, max 8 MB)
- MOA acknowledgement and captured electronic signature
- Private storage buckets and owner-only document viewing
- Owner can approve/reject bookings

## Important: not live until configured
This is a source-code starter, not a deployed/connected production service. In demo mode, the interface shows the two motorcycles, but secure accounts, real bookings, private uploads and shared availability are intentionally disabled. **Do not enter real personal information until Supabase is configured.**

## Set up Supabase
1. Create a new project in Supabase.
2. Open SQL Editor and run all of `supabase_setup.sql`.
3. In `index.html`, replace `PASTE_YOUR_SUPABASE_PROJECT_URL_HERE` and `PASTE_YOUR_SUPABASE_PUBLISHABLE_OR_ANON_KEY_HERE` with the project URL and publishable/anon key from your Supabase project settings. Never put the `service_role` key in browser code.
4. Host the folder using HTTPS, such as GitHub Pages or Netlify. Supabase Auth redirect URLs should include the hosted app URL.
5. Register an owner account through the app, then in Supabase SQL Editor run the following with that account's UUID from Authentication → Users:

   ```sql
   update public.profiles set role='admin' where id='YOUR-AUTH-USER-UUID';
   ```

6. Sign in using the Admin Login button. Confirm the dashboard loads and test a booking using a separate renter account.
7. If using email confirmation, configure the Supabase Auth Site URL and redirect URLs for the deployed website.

## Booking rules
- A booking is held while `pending` and blocks overlapping times. Once rejected, the time is available again.
- The renter who uploaded the license must personally collect the motorcycle and show the same original driver's license. No representative/substitute pick-up is allowed under the current policy.
- Owner must verify the renter's identity before release. Present the hardcopy MOA at pickup as well.
- Do not collect or store more personal information than necessary. Restrict owner account access, use MFA where available, and establish a retention/deletion policy for IDs and signatures.

## Before public launch
- Have the MOA and privacy notice reviewed for Philippine legal compliance, including the Data Privacy Act and applicable e-commerce/e-signature rules.
- Add the final complete rental rules: deposits, late returns, fuel, damage, accidents, cancellation/refund, prohibited use, towing/recovery, and dispute handling.
- Consider requiring email verification and MFA for owner access.
- Test double-booking, upload permissions, file size/type limits, mobile signing, and database policies with separate renter/admin accounts.
- Use a production-grade backend function to calculate the authoritative rental quote and validate booking requests. The browser-side price is an estimate and should not be treated as tamper-proof.
- Review the SQL policies carefully before real customer data is accepted. The included starter is not a substitute for a security audit.
