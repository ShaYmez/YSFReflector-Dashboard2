# Logo Directory

Place your logo image file here (e.g., logo.png, logo.jpg, logo.bmp, logo.webp, logo.gif).

The dashboard will automatically detect and use the logo file if it exists in this directory.

## Supported Formats

- PNG (.png)
- JPEG (.jpg, .jpeg)
- BMP (.bmp)
- WebP (.webp)
- GIF (.gif)
- SVG (.svg)

## Usage

1. Copy your logo file to this directory
2. Name it `logo` with any supported extension (case-insensitive)
3. The dashboard will automatically detect and display it

Example:
```bash
cp /path/to/your/logo.png img/logo.png
```

## Notes

- The logo should be in reasonable dimensions (e.g., 200x200px to 400x400px) for best results
- The image will be automatically scaled to fit within the header while maintaining aspect ratio
- File detection is case-insensitive (Logo.PNG, logo.png, LOGO.jpg all work)
- If multiple logo files exist, the first one found will be used
