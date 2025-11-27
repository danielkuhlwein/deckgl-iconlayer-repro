# DeckGL IconLayer Rendering Issue - Angular 19

Minimal reproduction project demonstrating IconLayer rendering failure after upgrading to Angular 19.

## Problem

After upgrading from Angular 18 to Angular 19, DeckGL's `IconLayer` no longer render on the map, while other layers like `ScatterplotLayer` continue to work normally.

### Symptoms

- ✅ **ScatterplotLayer**: Renders correctly (red circles visible)
- ❌ **IconLayer**: Does NOT render (blue camera icons missing)

## Environment

- **Angular**: 19.1.0
- **DeckGL**: 9.2.2
- **Mapbox GL**: 3.16.0
- **Node**: v25.2.1

## Reproduction Steps

1. **Install dependencies**
   ```bash
   npm install
   ```

2. **Add your Mapbox access token**
   - Sign up for a free account at https://account.mapbox.com/
   - Create an access token
   - Open `src/app/app.component.ts`
   - Replace `YOUR_MAPBOX_ACCESS_TOKEN_HERE` with your actual token

3. **Run the development server**
   ```bash
   npm start
   ```

4. **Open browser and check console**
   - Navigate to http://localhost:4200
   - You should see:
     - ✅ Red circles (ScatterplotLayer) - working
     - ❌ NO blue camera icons (IconLayer) - broken
   - Check console for diagnostic messages

## Expected vs Actual Behavior

**Expected:**
- Red circles from ScatterplotLayer
- Blue camera icons from IconLayer (slightly offset to the right)

**Actual:**
- Red circles render correctly
- Camera icons do NOT render at all

## Code Structure

- `src/app/app.component.ts`: Main component with Mapbox map and DeckGL overlay
  - Creates ScatterplotLayer (control/baseline)
  - Creates IconLayer with SVG camera icons (demonstrates the bug)
  - Console logs show expected vs actual behavior

## Workarounds Tested

### 2. Switch to MapLibre GL

Use MapLibre GL (open-source fork) instead of Mapbox GL. Testing shows MapLibre GL does not have this compatibility issue with Angular 19.

### 3. Downgrade to Angular 18

Revert to Angular 18 where the issue does not occur.

## Notes

- This is a **minimal reproduction** showing the issue only
- Default Angular 19 configuration is used
- The issue persists in Angular 20 zoneless mode (tested separately)
- The issue is specific to the Mapbox GL + DeckGL + Angular 19 combination
