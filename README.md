# Kitchen Card AI — Working MVP

This is a browser-based prototype for restaurants to create branded recipe cards without manually placing every text box.

## What it does

- Saves a restaurant brand profile
- Uses the restaurant's own name, logo, colors, and footer
- Accepts a food photo
- Accepts pasted recipe notes plus DOCX, PDF, RTF, TXT, MD, and CSV files
- Automatically separates common recipe sections
- Creates a live US-letter recipe-card preview
- Allows photo position, zoom, rotation, fit mode, and frame-height adjustment
- Allows logo size, placement, alignment, and logo-box width control
- Saves recipe cards in the browser
- Runs a basic quality-control checklist
- Exports PNG
- Opens a dedicated printable preview and prints or saves to PDF through the browser

## How to run

1. Unzip the folder.
2. Double-click `index.html`.
3. Open the **Brand** tab and set the restaurant name, logo, colors, and footer.
4. Return to **Builder**.
5. Upload a photo and paste a recipe.
6. Click **Generate Card**.
7. Proofread the card.
8. Save, export PNG, or use **Print / Save PDF**.

## Important MVP limitation

This version uses a local rules-based parser to demonstrate the workflow. A production version would connect to an AI API on a secure server to:

- Read Word and PDF recipe files more intelligently, including tables and scanned documents
- Understand rough chef notes more reliably
- Normalize ingredient quantities
- Rewrite pickup instructions in restaurant language
- Detect missing temperatures and yields
- Generate plating instructions from approved references
- Maintain multiple users and restaurant accounts
- Store images and cards in a cloud database
- Produce batch PDFs and ZIP files

Never place an API key directly inside this HTML file. The production app should use a server-side API route.

## Recommended production stack

- Next.js / React
- PostgreSQL or Supabase
- Object storage for photos and logos
- Server-side AI structured outputs
- Server-side PDF rendering
- User authentication and restaurant workspaces
- Revision history and approval workflow

## Version 7 Word-import improvements

- Preserves DOCX table rows and pairs ingredient names with quantities
- Removes Word table headers such as Amount and Qty
- Restores line breaks between numbered method steps
- Separates Yield and Station when Word places them on the same line
- Ignores duplicate early Chef Notes table headings

- Clears missing recipe sections when switching files, preventing old method, plating, notes, temperature, yield, or station content from carrying over.

## Version 13

This version was rebuilt from the stable Version 8 codebase.

Changes are intentionally limited to:

- Header name may be a station, restaurant, department, or left blank.
- PDF recipe upload has been removed.
- Recipe uploads accept DOCX, RTF, TXT, MD, and CSV.
- Existing Version 8 Word parsing and field-clearing behavior remain unchanged.

## Version 14

- New clears the visible photo and recipe filenames.
- Recipe upload displays the selected filename.
- Every Save creates a separate version snapshot.
- Library groups saved versions beneath each recipe title.
- Individual versions remain until manually deleted.
- New cards restart at Rev. 1.0.


## Version 15
Images and logos are stored in IndexedDB instead of localStorage, preventing version saves from failing when large photos fill the browser storage quota.

## Version 16

Internal-temperature detection now requires explicit finished-food wording. Oven, fryer, oil, grill, preheat, sous-vide, and holding temperatures are ignored. If no internal target is stated, the field stays blank.

## Version 17

The selected recipe filename now remains visible after the recipe is processed, even though the underlying browser file input is reset. Clicking New clears the displayed filename.

## Version 18

The native recipe upload control now keeps showing the selected filename after import. Clicking New clears the file input and removes the filename.

## Version 19

Added recipe-photo import:

- On supported phones, the rear camera can open directly.
- Existing recipe photographs can also be selected.
- Browser-based OCR reads the recipe and places the text into the recipe field.
- The normal card parser runs automatically after OCR.
- Users should proofread OCR results, especially quantities, fractions, and temperatures.

## Version 20

Recipe-photo OCR now uses explicitly configured worker, core, and language-file paths for better reliability on GitHub Pages and iPhone Safari. Progress and failure messages were improved.

## Version 21

Recipe-photo OCR improvements:

- Enlarges the image before OCR.
- Converts it to grayscale.
- Boosts contrast and cleans the paper background.
- Uses a single-block recipe-text recognition mode.
- Reports OCR confidence.
- Low-confidence text is left for correction instead of being automatically mapped into bad recipe fields.

## Version 22

Added a second card layout:

- Standard: title above a full-width food photograph.
- Split header: restaurant/logo/title information on the left and the food photograph on the right.

The layout is independent of the Classic, Modern, or Rustic visual style and is stored with brand settings and saved recipe versions.

## Version 23

Removed recipe-photo OCR and camera upload. The split header layout from Version 22 remains available.
