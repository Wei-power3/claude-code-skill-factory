# How to Use MarkItDown Converter v2.1.1

A step-by-step guide to converting PDFs and PowerPoint files to Markdown with preserved hyperlinks.

## 📚 Table of Contents

1. [Getting Started](#getting-started)
2. [Basic Usage](#basic-usage)
3. [Understanding Link Preservation](#understanding-link-preservation)
4. [Quality Metrics Explained](#quality-metrics-explained)
5. [Advanced Features](#advanced-features)
6. [Troubleshooting](#troubleshooting)
7. [Best Practices](#best-practices)

---

## 🚀 Getting Started

### Method 1: Download and Run Locally

**Step 1: Download**
```bash
# Clone the repository
git clone https://github.com/Wei-power3/claude-code-skill-factory.git

# Navigate to the skill
cd claude-code-skill-factory/generated-skills/markitdown-converter
```

**Step 2: Open in Browser**
- **Windows**: Double-click `index.html`
- **macOS**: Right-click `index.html` → Open With → Browser
- **Linux**: `xdg-open index.html`

**Step 3: Bookmark for Quick Access**
- Bookmark the file path in your browser
- Works offline - no internet required!

### Method 2: Direct Download

1. Visit: `https://github.com/Wei-power3/claude-code-skill-factory/tree/main/generated-skills/markitdown-converter`
2. Click on `index.html`
3. Click "Raw" button
4. Save page as HTML to your computer
5. Open the saved file in your browser

---

## 📝 Basic Usage

### Converting a Single File

**Step 1: Drag and Drop**
1. Open `index.html` in your browser
2. Drag a PDF or PPTX file onto the drop zone
3. Or click the drop zone to browse for files

**Step 2: Watch the Conversion**
- Progress bar shows conversion status
- Real-time quality metrics appear
- Processing time: ~2-5 seconds per MB

**Step 3: Download Results**
1. Click "⬇ Download Markdown" button
2. File saves as `filename_v2.1_links.md`
3. Or click "👁 Preview" to view in browser

### Batch Processing Multiple Files

**Drag Multiple Files**
1. Select multiple PDFs/PPTX files
2. Drag them all at once
3. Each file processes independently
4. Download each result individually

**Queue Management**
- Files process in parallel
- Stats show: Total, Processing, Completed, Failed
- Delete button removes completed jobs

---

## 🔗 Understanding Link Preservation

### How It Works

**Phase 2 implements intelligent link extraction:**

#### PDF Links
```
1. PDF.js extracts annotation objects
2. Filters for 'Link' subtype annotations
3. Retrieves URL or internal destination
4. Matches link to surrounding text using coordinates
5. Converts to markdown [text](url) format
```

#### PPTX Links
```
1. Unzips PPTX file structure
2. Parses XML slide content
3. Finds <a:hlinkClick> elements
4. Reads relationship file for rId → URL mapping
5. Matches hyperlink to associated text
6. Formats as markdown links
```

### Link Types Detected

**External Links:**
- HTTP/HTTPS URLs: `https://example.com`
- FTP links: `ftp://ftp.example.com`
- Email addresses: `mailto:user@example.com`

**Internal Links (PDF only):**
- Page references: `#page-5`
- Named destinations: `#section-abstract`
- Bookmarks: `#introduction`

### Example Conversions

**Before (PDF with link):**
```
Text with clickable link: "Visit our website"
Link annotation: https://example.com
```

**After (Markdown):**
```markdown
Text with clickable link: [Visit our website](https://example.com)
```

---

## 📊 Quality Metrics Explained

### The 4 Quality Dimensions

#### 1. Text Quality (0-100%)
**What it measures:**
- Ligature artifact removal (fi, fl, ff, ffi, ffl)
- Hyphenation repair (word- break → wordbreak)
- Spacing issue fixes
- Encoding problem resolution

**Scoring:**
- 90-100%: Excellent (< 5 artifacts)
- 70-89%: Good (5-15 artifacts)
- 50-69%: Fair (15-30 artifacts)
- < 50%: Poor (many issues)

#### 2. Structure Score (0-100%)
**What it measures:**
- Header detection (H1, H2, H3)
- List formatting (bullets, numbers)
- Bold/italic preservation
- Overall markdown richness

**Scoring:**
- 80-100%: Rich structure
- 50-79%: Moderate structure
- 30-49%: Basic structure
- < 30%: Plain text

#### 3. Links Preserved (Count)
**What it measures:**
- Total hyperlinks successfully converted
- External URLs preserved
- Internal references maintained

**Display:**
- Purple highlight color
- Shows actual count (not percentage)
- Tracked in global stats

#### 4. Overall Score (0-100%)
**Formula:**
```
Overall = (Text Quality × 0.5) + (Structure Score × 0.5)
```

**Interpretation:**
- 90-100%: Production-ready
- 70-89%: Minor cleanup needed
- 50-69%: Moderate editing required
- < 50%: Significant issues

### Quality Metrics Dashboard

```
┌────────────────────────────────────────┐
│  Text Quality  │  Structure  │  Links  │  Overall  │
│      95%      │     82%    │   12   │    88%   │
└────────────────────────────────────────┘
✅ Fixed 8 text artifacts
🔗 12/15 links preserved (80% preservation rate)
```

---

## 🔧 Advanced Features

### Previewing Results

**Browser Preview:**
1. Click "👁 Preview" on completed job
2. Opens new tab with formatted view
3. Shows quality metrics at top
4. Displays raw markdown in monospace
5. Links are clickable in preview

**What to Check:**
- ✅ Headers properly formatted?
- ✅ Lists correctly structured?
- ✅ Links clickable and accurate?
- ✅ Text clean and readable?

### Download Options

**Current Format:**
- Markdown (.md) with `_v2.1_links` suffix
- UTF-8 encoding
- Unix line endings (LF)

**Coming in Phase 4:**
- Plain text (.txt)
- HTML (.html)
- JSON (.json)

### Batch Statistics

**Global Stats Display:**
```
Total Files: 5
Processing: 1
Completed: 3
Failed: 1
Links Preserved: 47
```

**Per-Job Stats:**
- File size in KB
- Conversion timestamp
- Individual quality scores
- Error messages (if failed)

---

## ⚠️ Troubleshooting

### Common Issues

#### "File too large" Error
**Problem:** Browser runs out of memory

**Solution:**
1. Use desktop Python version for files > 50MB
2. Close other browser tabs
3. Use Chrome/Edge for better memory handling
4. Split large PDFs into smaller chunks

#### "No links found" in PDF
**Problem:** PDF doesn't have annotation objects

**Explanation:**
- Some PDFs have visual links but no annotations
- Scanned PDFs don't preserve clickable links
- Text-based PDFs with typed URLs work better

**Workaround:**
- Manually add links after conversion
- Use URL detection regex (coming in Phase 3)

#### PPTX Links Not Preserved
**Problem:** Old PPT format (not PPTX)

**Solution:**
1. Save as .pptx in PowerPoint
2. File → Save As → PowerPoint Presentation (.pptx)
3. Re-upload the PPTX file

#### "Conversion failed" Error
**Problem:** Corrupted or protected file

**Checks:**
1. File not password-protected?
2. File opens in PDF reader?
3. File size reasonable (< 50MB)?
4. File extension correct (.pdf/.pptx)?

### Browser Compatibility Issues

**Safari Users:**
- May need to enable "Allow JavaScript"
- Clear cache if conversion stalls
- Update to latest Safari version

**Firefox Users:**
- Some PDFs process slower
- Enable PDF.js in preferences
- Allow pop-ups for preview window

**Edge/Chrome:**
- Best performance and compatibility
- Recommended browsers

---

## 🎯 Best Practices

### For Best Results

**PDF Requirements:**
1. **Text-based PDFs** work best (not scanned images)
2. **Clean formatting** improves structure detection
3. **Standard fonts** reduce artifact issues
4. **Clickable links** must be annotation objects

**PPTX Requirements:**
1. **Modern .pptx format** (not old .ppt)
2. **Hyperlinks** added via Insert → Link
3. **Clean slide layouts** improve text extraction
4. **UTF-8 encoding** for special characters

### Document Types

**Excellent Results:**
- ✅ Research papers with citations
- ✅ Technical documentation
- ✅ Business presentations
- ✅ Academic reports
- ✅ Standard office documents

**Limited Results:**
- ⚠️ Scanned PDFs (no OCR)
- ⚠️ Complex multi-column layouts
- ⚠️ Heavy graphical content
- ⚠️ Protected/encrypted files

### Workflow Tips

**Batch Processing:**
1. Group similar document types
2. Process largest files first
3. Review quality metrics before downloading
4. Delete failed jobs to clean queue

**Quality Review:**
1. Always preview before downloading
2. Check link preservation rate
3. Verify structure detection
4. Test links in preview mode

**Post-Processing:**
1. Manual cleanup for < 70% quality
2. Add missing headers if needed
3. Format tables manually (Phase 2.2 coming)
4. Verify all links work

---

## 📚 Additional Resources

### Documentation
- **README.md**: Feature overview and setup
- **SKILL.md**: Claude skill integration
- **Examples/**: Sample files for testing

### GitHub Repositories
- **This Skill**: [claude-code-skill-factory/markitdown-converter](https://github.com/Wei-power3/claude-code-skill-factory)
- **Desktop Version**: [markitdown-desktop-converter](https://github.com/Wei-power3/markitdown-desktop-converter)

### External Libraries
- [PDF.js Documentation](https://mozilla.github.io/pdf.js/)
- [JSZip Documentation](https://stuk.github.io/jszip/)

### Support
- 🐛 Report issues on GitHub
- 💬 Ask questions in Discussions
- ⭐ Star the repo if helpful!

---

## 📅 Next Steps

After mastering v2.1.1, look forward to:

**Phase 3 (v2.2.0): Advanced PDF Features**
- Multi-column detection
- Header/footer removal
- Footnote extraction
- URL regex detection

**Phase 4 (v2.3.0): Export Formats**
- HTML export with CSS
- Plain text output
- JSON structured data
- Format selector UI

---

**Happy Converting! 🚀**