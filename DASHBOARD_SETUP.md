# Nyansa dashboard

The dashboard provides Best-6 planning, optional second-sitting grades and a shortlist. Its matcher and directory share the 66-institution dataset described in `INSTITUTION_DATA.md`; category ranges and inherited screening examples are not verified current cut-offs. Accreditation, programmes, requirements, streams and deadlines must be confirmed. Scholarship eligibility and deadlines are likewise subject to sponsor confirmation. The optional legacy detailed profile and older directory retain their prior datasets.

Matcher and essay drafts are saved to Supabase user metadata for signed-in email accounts, with a browser-only fallback scoped to the user/handle; guests remain browser-only. Drafts have a 5,000-character limit. Browser fallback is not protected against other users of the same device.

## Student Full Report

The GHS 29 student report uses Paystack card or mobile money. Checkout calls the deployed `verify-paystack` Edge Function and unlocks only when it returns `verified: true`. Device-stored references are rechecked before restoring access. Test payments unlock only a labelled test preview, not a paid licence.

If the Edge Function fails or rejects a reference, no new unlock is granted; the reference is kept for retry. See `PAYMENT_SETUP.md` for the required server and policy setup.

Counselor and partner payment/onboarding setup remains documented in `COUNSELOR_PAYMENTS.md` and `PARTNER_SETUP.md`.
