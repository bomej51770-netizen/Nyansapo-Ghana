# Counselor plan payments

Starter and Pro pricing cards offer Paystack checkout while retaining the demo flow. Guests may pay with an email address; signed-in users have their email prefilled and their purchase linked to their account. Checkout sends `product`, `plan`, `user_id` and `email` as Paystack metadata, and charges GHS 400 / 900 in pesewas. Test payments create test-only previews, never live paid licences.

## Required production configuration

1. Apply `supabase/payments_client_callback.sql` only if you accept that anonymous clients can forge payment records. Also run `supabase/counselor_workspaces.sql` for cohort saving.
2. Set `VITE_PAYSTACK_PUBLIC_KEY`, `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` at build time. Never put a Paystack secret or Supabase service-role key in frontend code.
3. Test with test credentials. Test callbacks are labelled previews and are not paid licences.

The browser callback now triggers a direct `success` insert and a device-local unlock without server verification. Both can be fabricated; do not use these records as proof of payment. If the insert is denied or fails, a warning is shown and the device-local unlock remains.

A local callback term lasts 90 days from the callback and is tied to the current browser. The counselor matcher's plan dropdown remains a planning control and is not a licence-enforcement mechanism.
