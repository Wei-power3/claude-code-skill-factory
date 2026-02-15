# MarkItDown Converter - Claude Skill v2.1.1

**Phase 2: Link Preservation** - Extract and preserve hyperlinks from PDFs and PowerPoint files.

## 🎯 Purpose

This Claude skill provides a **browser-based PDF & PowerPoint to Markdown converter** with intelligent structure detection and hyperlink preservation. Perfect for converting documents while maintaining clickable references.

## ✨ Key Features

### Phase 2: Link Preservation (NEW in v2.1.1)
- 🔗 **PDF Link Extraction**: Extracts clickable links using PDF.js annotations
- 📎 **PPTX Hyperlink Parsing**: Preserves hyperlinks from PowerPoint slides
- 🎯 **Smart Link Matching**: Spatially matches URLs to surrounding text
- ✨ **Markdown Formatting**: Converts to standard `[text](url)` format
- 📊 **Link Metrics**: Tracks links found vs. preserved in quality dashboard

### Core Features (from v2.1.0)
- 📐 **Font-Based Header Detection**: Analyzes font sizes for H1/H2/H3
- 📚 **Academic Section Recognition**: Auto-detects Abstract, Methods, Results, etc.
- 📋 **Intelligent List Detection**: Preserves bullet points and numbered lists
- **Bold/Italic Detection**: Maintains text emphasis from font names
- 🧹 **Text Cleaning**: Fixes ligatures, hyphens, encoding issues
- 📊 **Quality Metrics**: Real-time scoring of text quality and structure

### Privacy & Security
- ✅ **100% Client-Side**: All processing happens in browser
- ✅ **Zero Upload**: Files never leave your computer
- ✅ **No Tracking**: No analytics, cookies, or monitoring
- ✅ **Offline Capable**: Works without internet after download

## 🚀 Quick Start

### Option 1: Direct Use
1. Download `index.html` from this skill
2. Double-click to open in your browser
3. Drag & drop PDF or PPTX files
4. Download converted Markdown with preserved links

### Option 2: GitHub Pages
```bash
# Clone and serve
git clone https://github.com/Wei-power3/claude-code-skill-factory.git
cd claude-code-skill-factory/generated-skills/markitdown-converter
open index.html
```

## 📋 What's New in v2.1.1

### Link Preservation Features

**PDF Link Extraction:**
```javascript
// Extracts annotations from PDF pages
const annotations = await page.getAnnotations();
const links = annotations.filter(a => a.subtype === 'Link');
```

**PPTX Hyperlink Parsing:**
```javascript
// Reads relationship files to map rId → URL
const hyperlinks = xmlDoc.getElementsByTagName('a:hlinkClick');
const url = relationships[link.getAttribute('r:id')];
```

**Smart Link Matching:**
- Uses spatial coordinates to match links to text
- Tolerance-based matching for nearby text
- Fallback to hostname when no text match found

**Quality Metrics:**
- Links Found: Total hyperlinks detected
- Links Preserved: Successfully converted to markdown
- Link Preservation Rate: Percentage retained

## 🎯 Use Cases

### Academic Research
- Convert papers with preserved citations
- Maintain reference links to external sources
- Keep DOI and arxiv.org links clickable

### Technical Documentation
- Preserve API reference links
- Keep GitHub/StackOverflow references
- Maintain code repository links

### Business Presentations
- Convert decks with embedded URLs
- Preserve product/service links
- Keep social media handles clickable

## 📊 Quality Metrics

The converter provides 4-dimensional quality scoring:

| Metric | Description | Range |
|--------|-------------|-------|
| **Text Quality** | Artifact removal effectiveness | 0-100% |
| **Structure Score** | Markdown richness (headers, lists) | 0-100% |
| **Links Preserved** | Count of converted hyperlinks | 0-N |
| **Overall Score** | Weighted combination | 0-100% |

## 🔧 Technical Details

### Architecture
- **Frontend**: Vanilla JavaScript (no framework)
- **PDF Processing**: PDF.js 3.11.174
- **PPTX Processing**: JSZip 3.10.1
- **Link Extraction**: Native PDF.js + XML parsing
- **File Size**: ~60KB HTML (self-contained)

### Browser Support
- ✅ Chrome/Edge 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Opera 76+
- ❌ Internet Explorer

### Performance
- Processing Speed: ~2-5 seconds per MB
- Max File Size: ~50MB (browser-dependent)
- Memory Usage: ~100MB per file

## 📖 Usage Examples

### Example 1: Research Paper with Citations
```markdown
Input: paper.pdf (with DOI links)
Output: 
Recent studies [25](https://doi.org/10.1234/example) have shown...
For more details, see [GitHub repo](https://github.com/user/repo).
```

### Example 2: Business Presentation
```markdown
Input: deck.pptx (with website links)
Output:
Visit our [website](https://example.com) for more information.
Follow us on [Twitter](https://twitter.com/example).
```

### Example 3: Technical Documentation
```markdown
Input: manual.pdf (with API links)
Output:
See the [API documentation](https://api.example.com/docs) for details.
Check [StackOverflow](https://stackoverflow.com/questions/123) for examples.
```

## 🛠️ Integration with Claude

This skill can be referenced in Claude conversations:

```
# In Claude chat:
@markitdown-converter

User: "Convert this PDF and preserve all hyperlinks"
Claude: *uses skill to process PDF with link extraction*
```

## 📝 File Structure

```
markitdown-converter/
├── index.html          # Main converter application (v2.1.1)
├── README.md           # This file
├── HOW_TO_USE.md      # Detailed usage guide
├── SKILL.md           # Claude skill definition
└── examples/          # Sample files for testing
    ├── with-links.pdf
    └── with-links.pptx
```

## 🔗 Links & Resources

- **GitHub Repo**: [Wei-power3/claude-code-skill-factory](https://github.com/Wei-power3/claude-code-skill-factory)
- **Desktop Version**: [Wei-power3/markitdown-desktop-converter](https://github.com/Wei-power3/markitdown-desktop-converter)
- **PDF.js**: [mozilla/pdf.js](https://github.com/mozilla/pdf.js)
- **JSZip**: [Stuk/jszip](https://github.com/Stuk/jszip)

## 📄 License

MIT License - See LICENSE file for details

## 🙏 Credits

**Phase 2 Implementation:**
- PDF.js annotation API for link extraction
- Native XML parsing for PPTX hyperlinks
- Spatial coordinate matching algorithm

**Previous Versions:**
- List detection: Adapted from [jzillmann/pdf-to-markdown](https://github.com/jzillmann/pdf-to-markdown) (MIT)
- Text cleaning: Original implementation
- Structure analysis: Original implementation

## 📌 Version History

### v2.1.1 (2026-02-15) - Phase 2: Link Preservation
- ✅ PDF annotation link extraction
- ✅ PPTX hyperlink parsing
- ✅ Smart link-to-text matching
- ✅ Markdown [text](url) formatting
- ✅ Link count in quality metrics

### v2.1.0 (2026-02-15) - Phase 1: Structure Enhancement
- Font-based header detection
- Academic section recognition
- Intelligent list detection
- Bold/italic preservation
- Enhanced quality metrics

### v2.0.0 (2026-02-14) - Text Cleaning
- Ligature fixing
- Hyphenation repair
- Encoding normalization

### v1.0.0 (2026-02-13) - Initial Release
- Basic PDF/PPTX conversion
- Drag-and-drop interface
