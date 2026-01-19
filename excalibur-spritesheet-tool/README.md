# Excalibur Animation Builder

A web-based tool for creating and managing spritesheets and animations for [ExcaliburJS](https://excaliburjs.com/). This tool provides
an intuitive interface to parse spritesheets, define animations, and export configuration files ready to use in your Excalibur games.

## Features

- **Grid-Based Parsing**: Automatically parse regular spritesheets using grid configuration
- **Manual Frame Definition**: Build out SourceViews manually for each frame
- **Animation Creation**: Define animations with multiple frames, durations, and loop strategies
- **Live Preview**: Preview animations in real-time before exporting
- **Multiple Loop Strategies**: Support for `Freeze`, `End`, `Loop`, and `PingPong` animation modes
- **Export**: Save your animation configurations as a TS file
- **Code Preview**: Copy/Paste code directly from the web tool
- **ExcaliburJS Ready**: Export configuration in a format compatible with Excalibur's animation system

## Usage Guide

### 1. Load Your Spritesheet

Click the **Upload Spritesheet** button and select your spritesheet image. The image will be displayed on the canvas.

### 2. Parse Frames

Choose one of two parsing modes:

#### Grid Mode

For spritesheets with uniform, regularly-spaced frames:

1. Click **Grid Mode** button
2. Configure the grid settings:
   - **Sprite Width/Height**: Size of individual sprite frames (e.g., 32x32)
   - **Rows/Columns**: Grid dimensions (e.g., 4 rows × 4 columns)
   - **Origin Offset**: Starting position of the grid (default: 0,0)
   - **Margin**: Space between frames (if any)

The grid mode will automatically create frame definitions based on your configuration.

#### Manual Mode

For spritesheets with irregular frame layouts:

1. Click **Irregular (Manual)** button
2. Click the **+** Button under Source Views to add each frame individually
3. Modify as needed the x/y/w/h parameters to capture your frames

Frames are numbered sequentially (0, 1, 2...) and displayed on the canvas in green.

### 3. Create Animations

1. Enter an **Animation Group Name** (e.g., 'PlayerAnimations', 'NPCanimations', 'EnemyAnimations')

- adjust default duration if desired (in milliseconds)

2. Click **New Animation**
3. Select the animation from the list
4. Click **Add Frame** to add frames in sequence
5. For each frame:
   - Select the **Frame Index** from your parsed frames
   - Set the **Frame Duration** in milliseconds (e.g., 100ms for 10 FPS)
6. Set the **Loop Strategy**:
   - **Loop**: Animation repeats indefinitely
   - **PingPong**: Animation plays forward then backward
   - **Freeze**: Animation stops on the last frame
   - **End**: Animation plays once and stops

### 4. Preview Your Animation

- Select an animation from the list
- Click **Play** to preview
- Use **Pause** and **Reset** controls
- Adjust playback speed with the speed slider (0.25x to 2x)

### 5. Export Configuration

Click **Download Configuration** to export a JSON file containing:

- All frame definitions
- Animation configurations
- Animation group name (customizable at the top)

## Integration with ExcaliburJS

Once you've exported your configuration, you can use it in your Excalibur game:

```typescript
import animationConfig from "./animations.json";

// Create a spritesheet in Excalibur
const spritesheet = new ex.SpriteSheet({
  image: spriteImage,
  spriteDimensions: {
    width: 32,
    height: 32,
  },
  rows: animationConfig.rows,
  columns: animationConfig.columns,
});

// Define animations from your configuration
const animations: Record<string, ex.Animation> = {};

for (const anim of animationConfig.animations) {
  animations[anim.name] = spritesheet.getAnimation({
    frameOffset: anim.frames[0].frameIndex,
    frameCount: anim.frames.length,
    frameDuration: anim.frames[0].duration,
    loopStrategy: ex[anim.loopStrategy],
  });
}
```

## Tips for Best Results

- **Frame Uniformity**: For grid mode, ensure all frames are the same size with consistent spacing
- **Frame Ordering**: Number frames left-to-right, top-to-bottom in your spritesheet
- **Duration Testing**: Start with 100ms (10 FPS) and adjust based on your desired animation speed
- **Animation Names**: Use clear, descriptive names for animations (e.g., "idle_left", "walk_right")
- **Backup Exports**: Save your configuration files regularly for backup and version control

## File Management

- **Save Configuration**: Use the download button to save your animation config as JSON
- **Load Configuration**: Use the upload button to load a previously saved configuration
- **Load Spritesheet**: Upload a new spritesheet at any time; your animation definitions will remain

## Troubleshooting

**Frames not appearing on canvas**

- Ensure your image has loaded completely
- Check that grid dimensions don't exceed your spritesheet size

**Animation plays incorrectly**

- Verify frame indices are within the range of parsed frames
- Check that frame durations are in milliseconds
- Confirm the loop strategy matches your intended behavior

**Export file is empty**

- Ensure you've created at least one animation
- Add frames to your animations before exporting

## Technologies

- **React 19** - UI framework
- **TypeScript** - Type-safe development
- **Vite** - Build tool
- **Lucide React** - Icons

## License

MIT

```

```
