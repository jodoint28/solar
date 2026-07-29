# Florida Solar Savings

Spanish-language solar-savings lead-gen quiz landing page. Hosted at **solar-savings.info** (CNAME set).

## Stack
- Pure static HTML/CSS/JS — single `index.html`, no build step, no dependencies
- Google Maps Places API for address autocomplete (Step 6)
- HighLevel webhook for lead submission

## How to run
```
python3 -m http.server 5000
```
The "Start application" workflow runs this automatically on port 5000.

## Quiz flow (10 steps)
1. Homeowner? (yes/no)
2. ZIP code
3. Utility provider
4. Monthly bill slider
5. Sun exposure
6. **Address** — Google Places autocomplete with manual-entry fallback
7. Checking animation
8. Full name
9. Phone
10. Email → submits to HighLevel webhook

## Address step (Step 6)
- Google Maps JS API loaded in `<head>` via `initGooglePlaces` callback
- Uses `AutocompleteService` + `PlacesService` for custom dropdown UI (existing CSS classes: `.addr-suggestions`, `.addr-suggestion`)
- Restricted to `country: 'us'`, `types: ['address']`
- Collects `state.addressLat` / `state.addressLng` via `PlacesService.getDetails`
- If API fails to load within 6 s, status text switches to manual-entry mode — user can always continue without autocomplete

## HighLevel webhook
`https://services.leadconnectorhq.com/hooks/CLfmsC7D1pozIl8gemPI/webhook-trigger/3725de27-fda9-4fa0-8a0e-bca4af510d45`

Fields sent: `homeowner`, `zip`, `utility`, `bill`, `sun`, `address`, `addressLat`, `addressLng`, `fullName`, `phone`, `email`

## User preferences
<!-- Add preferences here as they come up -->
