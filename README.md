# Culdesac Tempe — Floor Plans Page

A standalone floor plan browser for Culdesac Tempe, built as a single `index.html` with no build step required. Runs locally in VS Code or any browser, and connects to the RentCafe API when a key is available.

---

## Repo Structure

```
culdesac-tempe/
├── index.html          ← the whole app
├── images/
│   ├── Acacia - Private Balcony 984 sq ft.jpg
│   ├── Acacia 984 sq ft.jpg
│   ├── Agave - Private Balcony 688 sq ft_2026.jpg
│   ├── Agave A.jpg
│   ├── barbary fig (combined).jpg
│   ├── chaparral.jpg
│   ├── Chicory - Semi-private Patio 908 sq ft.jpg
│   ├── Cholla 664 sq ft.jpg
│   ├── cholla a 656 sq ft.jpg
│   ├── cholla B 664 sq ft.jpg
│   ├── cholla c private balcony  664 sq ft.jpg
│   ├── Chuparosa 512 sq ft.jpg
│   ├── Desert Lily - 967-1021 SF.jpg
│   ├── golden barrel - Private Balcony.jpg
│   ├── Ironwood w_ sq ft.jpg
│   ├── Marigold (no balcony) 635 sq ft.jpg
│   ├── Marigold 635 sq ft.jpg
│   ├── Mariposa - 546 sq ft.jpg
│   ├── Mesquite -  880 sq ft.jpg
│   ├── Ocotillo - Private Balcony 648 sq ft.jpg
│   ├── Ocotillo 648 sq ft.jpg
│   ├── Palo Verde - Private Balcony 1035 sq ft.jpg
│   ├── Palo Verde 1035 sq ft.jpg
│   ├── prickly pear.jpg
│   ├── Saguaro 902 sg ft.jpg
│   ├── Senita w_ sq ft.jpg
│   └── Yucca 850 sq ft_2026.jpg
└── README.md
```

---

## Running Locally in VS Code

1. Install the **Live Server** extension (ritwickdey.liveserver)
2. Right-click `index.html` → **Open with Live Server**
3. Opens at `http://127.0.0.1:5500`

> ⚠️ Do **not** just double-click `index.html` to open it as a `file://` URL — images may not load due to browser CORS restrictions on local files. Use Live Server instead.

---

## Adding the RentCafe API Key

At the top of the `<script>` block in `index.html`, find:

```js
const API = {
  key:          null,              // ← paste RentCafe API key here
  base:         'https://basic.rentcafeapi.com',
  propertyCode: 'CULDESAC01',      // ← update with real propertyCode
};
```

1. Set `key` to your RentCafe API key string
2. Set `propertyCode` to the actual Culdesac Tempe property code from RentCafe
3. When a key is present, the app automatically calls:
   - `POST /floorplan/getfloorplans`
   - `POST /apartmentavailability/getapartmentavailability`
4. If the API call fails for any reason, it silently falls back to local data

---

## Floorplan → Image Mapping

All 27 image files map to 19 floorplan groups in `index.html`. Floorplans with multiple variants (e.g. Cholla has 4 variants, Acacia has 2) show a variant switcher in the detail modal and a gallery you can navigate left/right.

| Floorplan      | Type    | Sq Ft     | Variants |
|----------------|---------|-----------|----------|
| Chuparosa      | Studio  | 512       | 1        |
| Mariposa       | Studio  | 546       | 1        |
| Marigold       | 1 Bed   | 635       | 2 (w/ + w/o balcony) |
| Cholla         | 1 Bed   | 656–664   | 4 (A/B/C/standard) |
| Ocotillo       | 1 Bed   | 648       | 2 (standard + balcony) |
| Agave          | 1 Bed   | 688       | 2 (balcony + Agave A) |
| Prickly Pear   | 1 Bed   | TBD       | 1        |
| Chaparral      | 1 Bed   | 867       | 1        |
| Yucca          | 1 Bed   | 850       | 1        |
| Saguaro        | 1 Bed   | 902       | 1 (furnished) |
| Barbary Fig    | 2 Bed   | TBD       | 1 (combined) |
| Golden Barrel  | 2 Bed   | TBD       | 1        |
| Mesquite       | 2 Bed   | 880       | 1        |
| Chicory        | 2 Bed   | 908       | 1        |
| Ironwood       | 2 Bed   | TBD       | 1        |
| Senita         | 2 Bed   | TBD       | 1        |
| Desert Lily    | 2 Bed   | 967–1021  | 1        |
| Acacia         | 2 Bed   | 984       | 2 (standard + balcony) |
| Palo Verde     | 2 Bed   | 1035      | 2 (standard + balcony) |

---

## Things to Update

- [ ] Add `API.key` and correct `API.propertyCode`
- [ ] Add `API.propertyId` if using ID-based lookup instead of code
- [ ] Fill in `sqft` for Prickly Pear, Barbary Fig, Golden Barrel, Ironwood, Senita
- [ ] Fill in `priceFrom` for floorplans not yet in RentCafe (currently shows "Contact for pricing")
- [ ] Add unit-level room photos to each floorplan's `variants` array once available
- [ ] Update `availableUnits` arrays if not using live API
- [ ] Update apply URL once RentCafe application links are live
- [ ] Confirm bed/bath counts for Golden Barrel, Barbary Fig, Ironwood, Senita
