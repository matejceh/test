# Mobile Banking App Prototype

## Overview
A mobile banking app prototype built in a single HTML/CSS file (`app.html`) using an iPhone 16 frame (370×760px). A companion `design-system.html` documents all colors, typography, icons, and components. Data lives in `data.js`.

## Design System

### Colors
- Primary: `#2870ed` — buttons, icons, active states, links
- Text: `#444` — headings and body text
- Text muted: `rgba(68,68,68,0.8)` — labels, secondary text
- Background: `#f4f6fa` — app background
- Card background: `#fff`
- Success: `#028661` — positive amounts
- Danger: `#BC3B51` — errors, destructive actions
- Border: `#eee` / `#ddd`

### Typography
- Font: **Inter** (400, 500, 600, 700)
- Global `line-height: 1.4em` applied via `*` selector

#### Type Scale
| Element | Class | Size | Weight |
|---|---|---|---|
| Balance amount | `.balance-amount` | 30px | 700 |
| Balance currency (EUR) | `.currency` | 16px | 600 |
| Nav title | `.nav-title` | 16px | 600 |
| List value / IBAN / menu item | `.item-text` | 16px | 400 |
| Banner title | `.banner-title` | 14px | 500 |
| List label / Balance label | `.item-label` | 14px | 400 |
| Last transactions / See all | `.tx-title` / `.tx-see-all` | 14px | 400 / 600 |
| Package pill | `.package-pill` | 14px | 400 |
| Transaction amount | `.tx-amount` | 14px | 600 |
| Transaction currency (EUR) | `.tx-currency` | 12px | 600 |
| Banner description | `.banner-desc` | 13px | 400 |
| Transaction date | `.tx-date` | 12px | 500 (text-muted) |
| Transaction name | `.tx-name` | 12px | 500 |
| Action label | `.action-label` | 11px | 600 |
| Tab label | `.tab-label` | 9px | 600 |

### CSS Class Naming
- `.item-text` — general body/value text (16px/400), used for menu items, list values, IBANs, screen list items
- `.item-label` — muted caption/label (14px/400), used for field labels, account labels
- `.panel-header` — flex row for top of a panel card
- `.detail-row` — flex row for balance display
- `.section-header` — flex row for section title + see-all link

### Filter Tags
Used on statements screens. Tags and pill share a gray container (`background:var(--bg); border-radius:8px; padding:0 16px`).
- `.filter-tag` — active state: `background:#2870ed; color:#fff; border-radius:16px; border:1px solid transparent`
- `.filter-tag.off` — inactive: `background:#fff; color:#2870ed`
- `.filter-tags-wrap` — hidden by default (`max-height:0; overflow:hidden`), reveals on `.open` with `max-height:200px; padding:8px 0 12px`
- `.pill` — dropdown trigger row (`height:32px; background:var(--bg); border-radius:8px`); `.pill.open .pill-arrow` rotates 180°

### Payment Form Fields
Used on New payment, Quick pay, and Statements filter screens.
- `.pay-field` — column wrapper with `gap:8px`
- `.pay-field-label` — `14px/400`, `color:var(--text-muted)`
- `.pay-input` — `height:50px; border-radius:16px; border:1px solid var(--input-border); font-size:16px`; focus: `border:2px solid var(--primary)`
- `.pay-select` — same sizing as `.pay-input`, native `<select>` element; wrap in `position:relative` div with `padding-right:40px` and overlay `down-arrow.svg` at `right:16px` for custom arrow
- `.pay-input-wrap` — `position:relative; width:100%` wrapper for inputs

### Assets
All images and icons stored in `assets/`:
- `logo.svg` — Sparkasse logo (nav bar)
- `profile-ico.svg` — profile button icon
- `tab-account.svg`, `tab-card.svg`, `tab-offers.svg`, `tab-menu.svg` — tab bar icons (inline SVGs)
- `auth.svg` — Authorization quick action icon (business client)
- `new-pay.svg`, `photopay.svg`, `quick-pay.svg` — quick action icons
- `new-pay-primary.svg` — new payment icon in primary color variant
- `flik.svg` — Flik quick action icon (retail client)
- `details.svg` — account card menu button
- `down-arrow.svg` — balance dropdown + package pill arrow
- `eye.svg`, `eye-closed.svg` — balance visibility toggle
- `back.svg` — back button arrow
- `backspace.svg` — PIN screen delete key
- `banner.jpg` — banner background photo
- `mastercard.svg` — Mastercard logo
- `filter.svg` — filter icon (statements nav bar)
- `date.svg` — date input icon
- `pen.svg` — edit/change icon
- `more.svg` — more options icon
- `check.svg` — checkmark icon
- `check-account.svg` — account check icon
- `cancel.svg` — cancel icon
- `save-as-quick.svg` — save as quick payment icon
- `partners.svg` — partners icon
- `statements_documents.svg` — statements & documents icon
- `add-to-apple-wallet.svg` — Apple Wallet icon

**Menu icons** — stored in `assets/menu/`:
- `new-payment.svg`, `quik-pay.svg`, `photopay.svg`, `flik.svg` — Payments group (first 4)
- `sent-payments.svg`, `standing-orders.svg`, `partners.svg`, `e-invoices.svg`, `verify.svg` — Payments group (last 5)
- `accounts.svg`, `cards.svg` — Products group

---

## iPhone 16 Frame
- Frame: 370×760px, dark bezel, border-radius 54px
- Dynamic Island pill at top center — clicking opens a floating dev nav panel
- Side buttons: Action, Volume Up/Down (left), Power (right)
- Home indicator bar at bottom
- Screen area inset 14px on all sides, border-radius 42px

---

## Dev Nav
Clicking the Dynamic Island opens a floating panel with screen shortcuts.

**Main tabs:** Home, Cards, Offers, Menu

**Sub-pages — Home group:**
- Account detail, Transactions, Txn detail, Home (Company), Select client

**Sub-pages — Cards/Menu group:**
- Card detail, Card txns, Safety settings, Accounts list, Menu cards, Statements, Statements filter

**Payment flows:**
- Photo pay, Pay type, Quick pay, New pay, Review, PIN, Sent, Partners

**Utilities:** Language toggle (EN / SI), Dark mode toggle, Flow summary toggle

---

## Client Profiles

Two client profiles are supported, switchable via Select client screen:

### John Doe (retail)
- 2 accounts: My account + Savings account
- Actions: Photo pay, New payment, Quick pay, Flik (auth)
- Retail-level balances

### Company d.d. (business)
- 2 accounts: Company + Reserve account
- Actions: Photo pay, New payment, Quick pay, Authorization
- Business-level balances (284k / 95k)
- Main account label shows "Available balance" / "Current balance" in dropdown
- Card: Mastercard - Company d.d., limit 20.000 EUR

Switching clients re-renders carousel, cards, offers, and banner via `selectClient(index)`.

---

## Home Screen

### Account Carousel
Horizontally swipeable carousel with 2 account cards. Controlled by:
- Touch swipe (40px threshold)
- Clickable dot indicators below the card

#### Carousel behaviour
- Inactive slide: `visibility: hidden` + `pointer-events: none`
- Target slide shown before animation, outgoing slide hidden on `transitionend`
- `carousel-wrap` height set dynamically via `initCarousel()` and updated on slide change and balance dropdown toggle
- `initCarousel()` must be called after every `renderCarousel()` to refresh `slides` reference, reset position, and recalculate height
- Dot indicators: active 12px full primary, inactive 8px 50% primary

#### Account Card (each slide)
- White panel, border-radius 16px
- Account label + IBAN (`.item-text`)
- Details icon top right
- Available balance with show/hide toggle (blur via `color: transparent + text-shadow`)
- **Balance dropdown** — arrow button opens dropdown showing current balance; anchored right-aligned under the arrow button (`.balance-dropdown { right: 0 }`); arrow rotates 180° on open; `carouselWrap` height recalculated on toggle
- **Package pill** — opens absolute-positioned dropdown with package usage rows
- Last transactions list

### Quick Actions Row
- Renders from `appData.accounts[i].actions` array
- Action keys: `photopay`, `new-pay`, `quick-pay`, `auth`, `authorization`
- `new-pay` → `openPaymentType('home')`
- `quick-pay` → `openQuickPay('home')`
- Blue circle icons (50px), label 11px/600

### Banner
- Background photo (`banner.jpg`), border-radius 16px
- Text overlay: `rgba(68,68,68,0.8)` on `.banner-content`

---

## Payment Flow

**Entry points:** home "New payment" action OR menu "New payments" item → `openPaymentType(origin)`

```
Payment type screen → New payment (step 1) → Review (step 2) → PIN screen → Sent (step 3)
```

Back navigation:
- Payment type → home or menu (depending on origin)
- Step 1 → payment type screen
- Step 2 → step 1 (via `closeReview()`)
- PIN → step 2
- Step 3 → home (cancel or new payment)

---

## Payment Type Screen (`#payment-type-screen`)

### Nav
- Back button + "New payment" title

### Content
List of 4 payment types (`.item-text`, font-weight 400):
1. Payment in Slovenia
2. Foreign SEPA
3. VP70
4. Own account transfer

Clicking any type calls `selectPaymentType(type)` → `openNewPayment(origin)`

---

## Photo Pay Screen (`#photo-pay-screen`)

Dark fullscreen camera view with a scan frame (220×220px corner brackets) and animated scan line. Bottom area has "Import image" button and "Cancel" text button. Both close the screen via `closePhotoPay()`.

---

## Quick Pay Screen (`#quick-pay-screen`)

### Nav
- Back button + "Quick payments" title

### Content
List of 5 templates (`.item-text`, font-weight 400). Clicking any calls `selectQuickPay(index)` which opens New payment step 1 with all fields pre-filled.

**Templates:** Rent, Electricity, Gym, Internet, Loan repayment

---

## New Payment Screen (`#new-payment`) — Step 1

### Nav
- Back button + "New payment" title + step indicator (1. Prepare · 2. Review · 3. Sent)

### Content
Two groups (Pay from, Pay to, Payment) with labeled input fields.

### Navigation
- Back → Payment type screen
- Next (validate) → Review (step 2)

---

## Payment Review Screen (`#payment-review`) — Step 2

All fields read-only. "Pay" button → PIN screen.

---

## PIN / Authorization Screen (`#payment-pin`)

### Nav
- Back button + "Authorization" title

### Content
- "Enter PIN" label
- 6 circle indicators (empty `#eee`, filled `#ccc`)
- Numeric keypad (1–9, 0, delete with `assets/backspace.svg`)
- After 6 digits entered → Sent (step 3) after 300ms delay

### Navigation
- Back → Review (step 2), resets PIN

---

## Payment Sent Screen (`#payment-sent`) — Step 3

Confirmation screen. Actions: Save as quick pay, New payment, Cancel payment.

Cancel dialog: "Yes" button uses red text only (no red background).

---

## Select Client Screen (`#client-selector`)

### Nav
- Back button + "Select client" title

### Content
List of 2 clients with avatar circle (initial letter) + name + sub-label. Active client shown with checkmark.

**Clients:**
- John Doe — Personal account
- Company d.d. — Business account

`selectClient(index)` swaps `appData` via `clientDatasets[index]` and re-renders home.

---

## Cards Screen

### Nav Bar
Same as Home (profile icon + logo)

### Card List
Panels with card info. Tap → action sheet.

#### Card Action Sheet (iOS 26 Liquid Glass)
Options: Details, Transactions, Safety settings, Cancel.
- Overlay: `rgba(0,0,0,0.25)` + `backdrop-filter: blur(6px)`
- Sheet: `border-radius: 34px`, `backdrop-filter: blur(40px) saturate(180%)`

---

## Menu Cards Screen (`#menu-cards`)

Cards list accessible from Menu → Products → Cards. Same card list and action sheet as the Cards tab. Back → Menu tab. Uses `openMenuCards()` / `closeMenuCardSheet()`.

---

## Card Detail Screen (`#card-detail`)

Back + "Card details" title. Editable nickname (dialog). Safety settings shortcut. Monthly limit.

---

## Safety Settings Screen (`#safety-settings`)

Toggle rows: Block card, Online shopping, ATM withdrawals, Use outside Slovenia.

---

## Card Transactions Screen (`#card-transactions`)

Back + "Card transactions" title. Transaction list rendered into `#card-tx-list`. Opened via `openCardTransactions()` / `openCardTransactionsFromMenu()`.

---

## Offers Screen

Two promotional banners with `banner.jpg`.

---

## Menu Screen

Static HTML. Two groups inside panels.

### Payments group (9 items)
1. New payments → `openPaymentType('menu')`
2. Quick payments → `openQuickPay('menu')`
3. Photo pay
4. Flik
5. Sent payments
6. Standing orders
7. Partners
8. E-invoices
9. Verify online payments

### Products group (2 items)
1. Accounts → `openAccountsList()`
2. Cards → `openMenuCards()`

---

## Accounts List Screen (`#accounts-list`)

Back + "Accounts" title. Account list rendered into `#accounts-list-content`. Tapping an account opens an action sheet: Details → `accountListSheetDetails()`, Transactions → `accountListSheetTransactions()`.

---

## Account Detail Screen (`#account-detail`)

Back + "Account details". Editable nickname updates carousel label via `appData.accounts[activeAccountIndex].label`.

---

## Account Transactions Screen (`#account-transactions`)

Segment control: Waiting room | Archive (default) | Rejected. Opened from "See all" on home carousel.

---

## Transaction Detail Screen (`#transaction-detail`)

Three groups: Pay from, Pay to, Payment. Populated via `openTransactionDetail(accIdx, txIdx)`.

---

## Partners Screen (`#partners`)

List of saved payment partners. Selecting one pre-fills new payment form.

---

## Statements & Documents Screen (`#statements`)

### Nav
- Back button + "Statements & documents" title + filter icon button → `openStatementsFilterScreen()`

### Filter Area
Tags and pill share a gray container (`background:var(--bg); border-radius:8px; padding:0 16px`):
- Pill row ("Filter by type") toggles tag visibility via `toggleStatementsFilter()`
- Tags: TRR, Cards, Cash, Loans, Savings, Other — toggle via `toggleStatementsTag(el, category)`
- Active tags: blue fill; inactive: white fill; both have `border:1px solid transparent`

### Content
Flat list of document entries (`data-category` attribute). Active tag selection filters visible items.

---

## Statements Filter Screen (`#statements-filter`)

### Nav
- Back button + "Filter" title

### Content
Single panel with four fields:
1. **Date from** — `type="date"` opens system OS date picker
2. **Date to** — `type="date"` opens system OS date picker
3. **Document type** — `<select>` with options: All types, Statements, Contracts, Other; custom arrow overlay (`down-arrow.svg`)
4. **Subject / name of document** — text input

### Navigation
- Back button → `closeStatementsFilterScreen()` → returns to `#statements`
- "Filter" button (`.btn-main`) → same as back (dummy, no filtering logic)

---

## Statements 2 Screen (`#statements-2`)

Alternative statements screen variant with filter using toggle rows inside a pill dropdown instead of tag pills. Uses `openStatements2()` / `closeStatements2()` / `toggleS2Filter()` / `toggleS2Category(category, input)`.

---

## data.js

Exposes two global objects:

### `appData` (let — reassignable)
- `.accounts[]` — label, iban, available, current, balanceLabel?, currentLabel?, package, packageUsage, transactions, actions
- `.actionDefs{}` — map of action key → `{ icon, label }`
- `.cards[]` — name, type, number, validThru, outstanding, settlement, settlementDate, limit
- `.banners{}` — `{ home: {title, desc}, offers: [{title, desc}] }`

### `companyData`
Same structure as `appData` for the business client. Uses `appData.actionDefs` by reference.

### `clientDatasets`
Defined in `app.html` after data.js loads:
```js
const clientDatasets = [appData, companyData];
```
Used by `selectClient(index)` to swap `appData`.

---

## Shadows
- Panel / card: `4px 0 20px 0 rgba(68,68,68,0.1)`
- Dialog / action sheet: `0 8px 40px rgba(0,0,0,0.16)`

## Interaction
All press states use `:active` pseudo-class.

---

## Figma Reference
- File: Sparkasse (`UgGn7F6c30qKjLXcDty8eg`)
- Home: node-id `2125-523`
- Cards: node-id `2021-1622`
- PIN screen: node-id `2690-674`
- Statements filter: node-id `2786-1509`

---

## Screens Status
- [x] Home (`app.html`)
- [x] Cards (`app.html`)
- [x] Menu cards (`app.html`)
- [x] Card detail (`app.html`)
- [x] Card transactions (`app.html`)
- [x] Safety settings (`app.html`)
- [x] Photo pay (`app.html`)
- [x] Payment type screen (`app.html`)
- [x] Quick pay screen (`app.html`)
- [x] New payment step 1 (`app.html`)
- [x] Payment review step 2 (`app.html`)
- [x] PIN / Authorization screen (`app.html`)
- [x] Payment sent step 3 (`app.html`)
- [x] Select client (`app.html`)
- [x] Partners (`app.html`)
- [x] Accounts list (`app.html`)
- [x] Offers (`app.html`)
- [x] Menu (`app.html`)
- [x] Account detail (`app.html`)
- [x] Account transactions (`app.html`)
- [x] Transaction detail (`app.html`)
- [x] Statements & documents (`app.html`)
- [x] Statements filter (`app.html`)
- [x] Statements 2 (`app.html`)
- [x] Design system (`design-system.html`)
