// Serverless function for Vercel - CommonJS format

module.exports = async function handler(req, res) {
  // Enable CORS
  res.setHeader('Access-Control-Allow-Credentials', true);
  res.setHeader('Access-Control-Allow-Origin', '*');
  res.setHeader('Access-Control-Allow-Methods', 'POST, OPTIONS');
  res.setHeader('Access-Control-Allow-Headers', 'Content-Type');

  if (req.method === 'OPTIONS') {
    res.status(200).end();
    return;
  }

  if (req.method !== 'POST') {
    return res.status(405).json({ error: 'Method not allowed' });
  }

  try {
    const { image, imageType, fixtureType } = req.body;

    console.log('Received request:', {
      hasImage: !!image,
      imageType,
      fixtureType,
      imagePrefix: image ? image.substring(0, 30) : 'none'
    });

    if (!image || !fixtureType) {
      return res.status(400).json({ error: 'Missing image or fixture type' });
    }

    // Determine media type - support all common image formats
    let mediaType = 'image/jpeg'; // default
    let imageData = image;

    // Extract data URL if present
    if (image.startsWith('data:')) {
      const match = image.match(/data:(image\/[^;]+);base64,(.+)/);
      if (match) {
        mediaType = match[1];
        imageData = match[2];
      } else {
        // Fallback: just remove the prefix
        imageData = image.split(',')[1] || image;
      }
    }

    // Override with explicitly provided imageType if available
    if (imageType && imageType.startsWith('image/')) {
      mediaType = imageType;
    }

    // Map to Claude-supported formats
    const supportedTypes = {
      'image/jpeg': 'image/jpeg',
      'image/jpg': 'image/jpeg',
      'image/png': 'image/png',
      'image/gif': 'image/gif',
      'image/webp': 'image/webp'
    };

    mediaType = supportedTypes[mediaType.toLowerCase()] || 'image/jpeg';

    console.log('Processed media type:', mediaType);

    const CLAUDE_API_KEY = process.env.CLAUDE_API_KEY;

    if (!CLAUDE_API_KEY) {
      return res.status(500).json({ error: 'API key not configured' });
    }

    const RUBRIC = `
You are a visual merchandising auditor for Equinox Shop retail locations. Evaluate the uploaded photo and provide a scored assessment.

OUTPUT FORMAT (strictly follow this):
SCORE: [number]/100

BREAKDOWN:
✓ [Category]: [X]/[XX] pts - [brief explanation]
✗ [Category]: [X]/[XX] pts - [brief explanation]
⚠ [Category]: N/A - Cannot evaluate from photo

CRITICAL FORMATTING RULES:
1. Include ALL scoring categories in the breakdown
2. If you cannot evaluate a category from the photo, use: "⚠ [Category Name]: N/A - Cannot evaluate from photo"
3. Do NOT penalize the score for categories marked N/A
4. Do NOT use "---" or "##" or leave blank lines in the breakdown
5. Every breakdown line must start with ✓, ✗, or ⚠

TOP FIXES:
1. [Specific actionable fix]
2. [Specific actionable fix]
3. [Specific actionable fix]
4. [Specific actionable fix]
5. [Specific actionable fix]

WHAT'S WORKING:
- [Brief positive observation]
- [Brief positive observation]

SCORING RUBRIC FOR BAGS:
- Quantity (25 pts): Appropriate number for shelf size, not overcrowded or sparse
- Visual Arrangement (40 pts): Bags nested/overlapping, varying heights, clear focal point
- Color Story (25 pts): Color progression visible, coordinates with nearby merchandise
- Organization (10 pts): Grouped by similarity, not random

SCORING RUBRIC FOR SHOES:
- Display Basics (35 pts): Left shoes only, one per style, clean presentation
- Grid Pattern (40 pts): Organized in sets of 2-3, mix of angles, clear layout
- Visual Interest (25 pts): Variation between shelves, use of risers if visible

SCORING RUBRIC FOR WOMEN'S WALL:
- Outfit Structure (35 pts): Complete outfits (top + bottom), coordinated colorways, consistent sizing
- Color Flow (35 pts): Light to dark gradient, logical progression, ends with black
- Separation (20 pts): Categories clearly divided, no mixing of lounge/performance
- Styling (10 pts): Accessories match theme, faceouts coordinate with display below

SCORING RUBRIC FOR MEN'S WALL:
- Category Flow (30 pts): Logical progression, categories separated, not bunched
- Color Organization (30 pts): Light to dark within sections, intentional groupings, visual rhythm
- Clean Presentation (25 pts): Straight bars, organized appearance, proper spacing
- Fixture Integrity (15 pts): Only apparel on apparel fixtures, no bags/accessories mixed in

Focus on what's VISIBLE. If you can't verify something, mark it N/A but don't penalize. Be direct and actionable.
`;

    console.log('Making API call to Claude...');

    const response = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: {
        'x-api-key': CLAUDE_API_KEY,
        'anthropic-version': '2023-06-01',
        'content-type': 'application/json'
      },
      body: JSON.stringify({
        model: 'claude-sonnet-4-5-20250929',
        max_tokens: 2000,
        messages: [{
          role: 'user',
          content: [
            {
              type: 'image',
              source: {
                type: 'base64',
                media_type: mediaType,
                data: imageData
              }
            },
            {
              type: 'text',
              text: `Evaluate this ${fixtureType} display.\n\n${RUBRIC}`
            }
          ]
        }]
      })
    });

    const data = await response.json();

    console.log('API Response status:', response.status);

    if (!response.ok) {
      console.error('Claude API Error:', JSON.stringify(data, null, 2));
      throw new Error(data.error?.message || `API error: ${response.status}`);
    }
    
    return res.status(200).json({
      evaluation: data.content[0].text
    });

  } catch (error) {
    console.error('Error occurred:', error.message);
    console.error('Error stack:', error.stack);
    return res.status(500).json({ 
      error: error.message || 'Analysis failed'
    });
  }
};
