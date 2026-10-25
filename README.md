# History Supply Checker

Frontend for PIC review of vessel requisition supply history.

- Live webhook: `https://mataram9.app.n8n.cloud/webhook/history-checker`
- n8n workflow: History Supply Checker (DeepSeek Configured)

Upload a PDF on the page; it POSTs multipart form data to the n8n webhook and renders the JSON response.

## Ready-to-use flow (no AI)
- UI posts to `https://mataram9.app.n8n.cloud/webhook/history-checker` (editable in ⚙ settings, saved in localStorage; blank = offline preset).
- PDF upload: text is extracted in-browser (pdf.js) and sent as multipart `text` + `file`; n8n `Parse Requisition` parses Beesuite FM.OPS.01 layout.
- No PDF: JSON `{vessel_name, request_date, items:[...]}` (parser skipped).
- n8n: Webhook → Parse Requisition → Get Generic → Get History (single full-sheet read each) → Build Payload (classify STOCK/PI/PO/PR/UR, top 3) → Respond.
