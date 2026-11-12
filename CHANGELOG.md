# B-Editor Release Notes

Learn about changes to B-Editor.

## B-Editor 1.0 Beta Release Notes

Build `26A0134i`, released November 12, 2026.

Write, build, run, debug, and deploy the B-Human code from one native Mac app.

### Overview

B-Editor 1.0 includes Sparkle 2.10.1 and uses clangd and lldb-dap from Xcode. B-Editor 1.0 supports the SimRobot and Booster schemes in Debug, Develop, and Release. B-Editor 1.0 requires a Mac running macOS 27 or later, Xcode 27, and a B-Human checkout with its submodules.

In Beta 1, the simulation canvas, hot swap, and the live behavior views need B-Human changes that aren't public yet. Everything else works in a normal B-Human checkout. The team gets these changes as a simulation patch package (`sim-patch-<commit>.zip`). It changes only the files of your checkout and doesn't commit anything, and `revert.sh` removes it again. See Simulation.

See Deploy to learn more about the state of real robot support.

#### General

**First launch:** B-Editor is not notarized. On the first launch, open System Settings, choose Privacy & Security, and click Open Anyway.

##### New Features

- B-Editor is a native Mac IDE for the B-Human code that looks and works like Xcode. (26A0122.001)
- The new Set Up window checks for Xcode, clangd, lldb-dap, Git, CMake, Ninja, and the Git submodules on first launch. (26A0122.002)
- The Set Up window now shows a command you can copy for missing CMake, Ninja, or submodules. You can choose the repository there, check again, and move the app to Applications. (26A0122.003)
- You can now open the Set Up window at any time with Check Setup in the Help menu. It checks your tools again when it opens. (26A0122.211)
- You can now open a checkout with Open Folder (Command-O). A folder that isn't a B-Human repository shows an alert. (26A0122.004)
- B-Editor now saves open files when it quits. (26A0122.005)
- Files that changed on disk now reload when you return to the app. (26A0122.006)
- When a file with unsaved edits also changed on disk, a dialog now offers Use Version on Disk, Compare, and Keep My Version. It appears when you return to the app, and before a save or quit would overwrite the file. (26A0122.212)
- B-Editor now keeps a copy of your unsaved changes every 15 seconds and when you switch to another app. After an unexpected quit, the next launch offers Recover and Discard. Recover opens the files with your edits unsaved. (26A0122.213)
- The app is now called B-Editor. Your settings, bookmarks, recovery data, and updates carry over. (26A0122.214)
- B-Editor now reopens the files of your last session for each repository. You can turn this off in Settings. (26A0122.007)
- The new About window shows the build, and it opens the acknowledgments and the license. (26A0122.008)
- The Help menu now links to these release notes. (26A0122.009)
- The About window now also shows the release date and the compatibility. For Alpha, Beta and RC builds, it shows the stage as a colored capsule. (26A0122.215)
- The new Send Feedback in the Help menu opens a form for a bug or a wish. For a bug, it asks what happened, what you expected, and the steps to reproduce it. (26A0122.216)
- Send Feedback now adds the build, the macOS version, the Mac model, and the date. It can include the logs and a screenshot of the editor, and Show Everything shows the full text. (26A0122.217)
- Continue in Browser now opens a prefilled GitHub issue and shows the attachments in the Finder, so you can drag them into the issue. (26A0122.218)
- Animations now follow the Reduce Motion setting in Accessibility. (26A0122.219)
- Alerts now open as sheets on the editor window, also when the window is in the background. (26A0122.220)
- B-Editor has a new app icon, built in Icon Composer with Liquid Glass. Alpha builds have a red icon, Beta builds an orange one, and RC builds and releases a dark one. (26A0122.221)
- The new Discord settings can show what you work on as your Discord activity, for example "Editing BPRPerceptor.cpp". It is off by default. You choose how much it shares, which repositories it hides, and the buttons friends see. Pause Discord Activity in the Editor menu stops it for the session, and a button next to the branch shows its state. (26A0122.222)
- The Discord activity talks only to the Discord app on your Mac, and it tries again every 15 seconds while Discord is closed. (26A0122.223)

##### Known Issues

- The app is not notarized, so macOS blocks the first launch. (26A0122.010)

  **Workaround:** Open System Settings, choose Privacy & Security, and click Open Anyway.

- A copy started from the disk image can't update itself. (26A0122.011)

  **Workaround:** Drag the app to Applications. The Set Up window also offers Move to Applications on first launch.

#### Build System

##### New Features

- You can now build SimRobot and Booster with Build (Command-B). It runs `xcodebuild` for the selected scheme. (26A0122.014)
- Build now runs `Make/macOS/generate` first. You can turn this off with Generate the project before building in the General tab of Settings, and Build still generates the project when none exists. (26A0122.226)
- The new Generate Project (Control-Command-G) in the Product menu runs `Make/macOS/generate` and then updates the compile database. (26A0122.227)
- The new scheme menu in the toolbar lists every SimRobot and Booster scheme in each configuration. (26A0122.015)
- The new destination menu lists SimRobot scenes by robot type and your recent scenes. For Booster, it lists teams and robots. (26A0122.016)
- You can now build and start the selected destination with Run (Command-R). Run Without Building (Control-Command-R) skips the build, and Stop (Command-.) ends the run. (26A0122.017)
- The toolbar now shows build progress as compiled files out of all files. (26A0122.018)
- Build now saves modified files first. You can turn this off in Settings. (26A0122.019)
- The new Issues navigator lists errors and warnings from the build log. Its Live segment shows findings from clangd and the shell check while you type. (26A0122.020)
- The Issues navigator also lists linker errors, with the name of each undefined or duplicate symbol. (26A0122.021)
- Next Issue and Previous Issue now step through build issues and live findings. (26A0122.022)
- The build log now says when `Make/macOS/generate` fails because submodules are missing. (26A0122.023)
- You can now remove the build products with Clean Build Folder (Shift-Command-K), after a confirmation. (26A0122.024)
- The counts in the toolbar now include the live results of clangd before any build. The count chips have a new look. (26A0134.001)
- The filter tabs of the Issues navigator now have the same width. (26A0134.002)

#### Config Editor

##### New Features

- `.cfg` files under `Config/` now open as a table, with a switch to their source. (26A0122.025)
- You can now edit values in the table, and booleans have a popup. The table refuses a value that would break the syntax of the file. (26A0122.026)
- The table now reads the type of each value from the C++ headers. The Type column shows it, and an enum has a popup that lists its values with their documentation. (26A0122.228)
- The table now checks a new value against its type. A wrong value isn't written, and a card under the field says what the type expects, such as a whole number, true or false, or an angle like 90deg. (26A0122.229)
- You can add entries and sub-entries, delete, rename, and change the type of a key. All of these actions support undo. (26A0122.027)
- Each row now has a context menu with Add Entry, Add Sub-Entry, Delete Entry, and Show in Source. (26A0122.028)
- You can now double-click a key to rename it. Tab moves from the key to its value. (26A0122.029)
- You can now work in the table with the keyboard: (26A0122.030)
  - The arrow keys move, collapse, and expand rows.
  - Return edits a value.
  - Delete removes an entry.
- The new filter field shows only matching rows. (26A0122.031)
- A file that doesn't parse now shows the line and column of the error, and a button that opens the source. (26A0122.032)
- `Robots/robots.cfg` and each `network.cfg` are now read-only in the table and in the source, because they are generated. A lock in the jump bar and a note in the bar above the file say so. (26A0122.033)
- The new Compare With popup in the table bar shows how a file differs from another file. (26A0122.034)
- The Document inspector now shows the search order of a file, and a banner above the editor warns when a file is hidden or unused. (26A0122.035)
- The search order now also covers Remote and Replay scenes. It marks the folders that the robot or the log chooses when it connects or opens. (26A0122.230)
- When you select a row, Quick Help in the Document inspector now shows its declaration, documentation, type, values, and default from the C++ header. It links to the declaration and to the module that loads the file. (26A0122.231)
- The new Override In menu in the bar above a `.cfg` file copies the file into another location or scenario and opens the copy. An existing file is never replaced. (26A0122.232)
- New Location and New Scenario in the Override In menu now create a folder in `Config/Locations` or `Config/Scenarios`, based on another one, and copy the files you choose. (26A0122.233)
- `threads.cfg` now opens as a table of representations with a provider popup. Same Entry In changes other scenarios too, even when their files are closed. (26A0122.036)
- The `threads.cfg` table now offers multiple features: (26A0122.037)
  - The Scenarios column shows how many scenarios use each entry.
  - Add Representation has a search field and a choice of providers.
  - Remove deletes the selected entry.
  - The Document inspector links to the header of the selected representation.
- `threads.cfg` files of a scenario are now checked against the rules of the module graph. A representation provided twice in one thread and a requirement without a provider appear as warnings in the Issues navigator and in the table. (26A0122.234)
- A missing provider now appears as a row in the `threads.cfg` table, with a menu that adds a module that provides it. The warning in the Issues navigator has the same fix. (26A0122.235)
- A `threads.cfg` requirement that several other threads provide is now an error instead of a warning. (26A0134.003)
- The new Compare Scenarios in the Navigate menu, and Compare With Scenario in the bar of a `threads.cfg` file, compare two scenarios for K1 or T1. Modules lists provider differences, Values lists the `.cfg` keys that resolve to different values with the search order of each scenario, and Files lists files that only one scenario has. (26A0134.004)
- `armKeyFrameEngine.cfg` of K1 and T1 has a new Motion Preview tab that plays any arm motion on a 3D robot without a simulation. It shows the states as orange ghost poses, the joint angles, stiffness, and limits, and the interpolation curve of the active state. (26A0134.005)
- The motion preview plays at 0.25x, 1x, or 2x, loops, restarts, and scrubs. It shows the right, the left, or both arms, and you can drag to turn the robot. (26A0134.006)
- While a motion plays, the source marks the state at the playhead, and edits show on the robot at once. (26A0134.007)
- A play button in the gutter next to each motion `id`, and Preview Motion in the Navigate menu (Control-Option-Command-P), open the motion preview. (26A0134.008)
- Resting the pointer on an `angles` line shows the pose of that state, with Open Player. (26A0134.009)
- The motion preview warns about joint angles beyond `jointLimits.cfg`, a duration under 10 ms, a wrong number of angles or stiffness values, and an unknown interpolation. (26A0134.010)
- The new Module Graph in the Navigate menu draws the modules and representations of the repository. Solid lines are `REQUIRES`, dashed lines are `USES`, and colors show the threads. You can filter by thread and depth, and a double-click opens the header of a module or focuses a representation. (26A0122.236)
- The new Representations in the Navigate menu lists every representation with a filter. It shows the header, the providers in the current scenario, and the drawings of a representation. (26A0122.237)
- The Document inspector now has Show in Module Graph for a module and for a representation. (26A0122.238)

#### Debugging

##### New Features

- You can now run SimRobot through `lldb-dap` with Run, and end it with Stop. The SimRobot tab shows its output. (26A0122.042)
- Stop now ends SimRobot after about 3 seconds if `lldb-dap` doesn't. (26A0122.043)
- The new Debug menu contains Pause and Continue (Control-Command-Y), Step Over (F6), Step Into (F7), and Step Out (F8). The debug bar shows Continue and the step buttons while SimRobot is paused. (26A0122.044)
- You can set a breakpoint by clicking the gutter or with Toggle Breakpoint at Line (Command-Backslash). Right-click a breakpoint to open its options. (26A0122.045)
- Breakpoints now support conditions, a robot and role filter, an ignore count, and automatic continue. (26A0122.046)
- Breakpoints can now log a message or run a debugger command when they're hit. Text between two `@` signs in a message is evaluated as an expression. (26A0122.240)
- The plus menu at the bottom of the Breakpoints navigator now creates a Symbolic Breakpoint or a C++ Exception Breakpoint. (26A0122.241)
- A symbolic breakpoint now stops at a function by name, in all modules or in one module. It supports a condition, an ignore count, actions, and automatic continue. (26A0122.242)
- The new C++ Exception Breakpoint stops when an exception is thrown, caught, or both. (26A0122.243)
- B-Editor now stores breakpoints for each repository and offers the robots it has seen in the filter. (26A0122.047)
- The new Breakpoints navigator lists your breakpoints. Click a tag to enable or disable it, double-click to edit it, or press Delete to remove it. (26A0122.048)
- You can now turn all breakpoints on or off with Activate Breakpoints (Command-Y). They stay in place. (26A0122.049)
- The new Debug navigator groups threads by robot and shows system threads in their own group. (26A0122.050)
- While SimRobot is paused, you can now expand any robot thread in the Debug navigator to load its frames. (26A0122.244)
- The Debug navigator now shows the process ID with CPU and memory gauges, which update every 2 seconds. (26A0122.051)
- When SimRobot stops, the editor now shows the first frame with source code and marks the execution line. Click another frame to show its line and variables. (26A0122.052)
- The debug bar now shows the robot, role, and selected frame. (26A0122.053)
- The new variables pane shows expandable values, with a scope popup and a filter. Auto shows arguments and locals, and Globals and Registers load when you choose them. (26A0122.054)
- The filter in the variables pane now also searches nested values. It matches names, types, and values up to 6 levels deep and stops after 5000 values. (26A0122.245)
- The variables pane now has a Watch section. Add an expression with Add Expression, or choose Add to Watch in the context menu of a variable. Watches persist for each repository. (26A0122.246)
- You can now change a simple value while SimRobot is paused. Double-click the variable or choose Edit Value. (26A0122.247)
- While SimRobot is paused, a data tip now shows the value of the variable or selected expression under the pointer. You can expand it, edit a value, and add it to the watches. (26A0122.248)
- The new lldb console runs plain lldb commands such as `p x` and `bt` in the selected frame. The Up and Down keys step through your history. (26A0122.055)
- Debug sessions now apply the Xcode data formatters of the repository as lldb type summaries. (26A0122.056)
- The debug bar now has the flat Xcode style, with the step buttons next to the robot, role, and frame. (26A0122.249)
- The debug area footer now keeps its labels on one line. (26A0122.250)

##### Resolved Issues

- Fixed: A SimRobotHost stayed stopped when the debug adapter ended while attached to it. The editor now resumes the host. (26A0122.251)

##### Known Issues

- While SimRobot.app runs instead of the canvas, or while the canvas is hidden and SimRobot.app isn't running, the SimRobot tab shows output only. You type console commands in SimRobot itself. The `.con` editor completes and checks commands but doesn't send them. (26A0122.057)
- A filter with only a robot uses the Cognition role, and a filter with only a role uses the first robot. (26A0122.059)
- System threads in the Debug navigator show no frames. (26A0122.061)

#### Deploy

##### New Features

- The new Deploy sheet (Shift-Command-D) edits team presets and assigns robots to numbers with drag and drop. Dropping on a taken number swaps the robots, and dropping on the background removes one. (26A0122.063)
- You can now add, duplicate, rename, and delete presets. (26A0122.064)
- Cancel in the Deploy sheet now undoes the changes to presets and robot assignments since the sheet opened, also the ones already written to disk. (26A0122.252)
- Presets now contain multiple settings: (26A0122.065)
  - Team, shown by name for known teams
  - Field player and goalkeeper colors
  - Scenario and location
  - Magic number, with automatic as the default
  - Wireless profile
  - Volume
- The sheet now selects the build configuration, and its footer previews the command it runs. (26A0122.066)
- The new Robots mode contains the options Build before deploying, Restart bhuman, and Delete logs. They persist between launches. (26A0122.067)
- The new robot table shows live LAN and WLAN state, battery, temperature, logs, calibration, and crashes. It also shows the host and the state of the bhuman service. (26A0122.068)
- The new Substitutes section lists the robots that aren't in the preset. (26A0122.069)
- Each robot now uses the faster of LAN and WLAN. Before a deploy, B-Editor pings for up to 2.5 seconds to find robots. (26A0122.070)
- The new robot menu contains multiple actions: (26A0122.071)
  - Login
  - Connect SimRobot
  - Show Crash Log
  - Download Calibration
  - Start, Restart, and Stop
  - Shutdown, after a confirmation
- An action from the robot menu that fails now shows an alert with the reason, such as a robot that can't be reached over SSH. (26A0122.253)
- You can now download or delete the logs of reachable robots in Logs mode. (26A0122.072)
- You can now open logs in SimRobot with Open in SimRobot in Logs mode, or in the context menu of a `.log` file in the Project navigator. B-Editor then builds and runs the Replay scene with those logs. (26A0122.254)
- Run with a Booster destination now deploys to the selected team or robot. (26A0122.073)
- You can now cancel a running deploy from the toolbar. (26A0122.074)
- The new Robots sidebar keeps your robots in view while you work. (26A0122.075)
- The Robots sidebar now shows the battery level and the ping of each robot. The ping is colored by how good it is. (26A0134.011)

##### Known Issues

- Deploy, robot monitoring, the robot menu, and log download haven't been tested on real robots. (26A0122.076)

  **Workaround:** If the editor fails, use the Qt DeployDialog.

- Shutdown reports a failure only when the robot can't be reached over SSH. (26A0122.077)

#### Files

##### New Features

- You can now create a file from a template with New File (Command-N). The plus button in the navigator opens the same sheet. (26A0122.080)
- The New File sheet contains multiple templates: (26A0122.081)
  - Module, which can add its entry to `threads.cfg`
  - Representation, with or without a `.cpp` file
  - Option and Inline Option
  - Thread and Class
  - C++ File and Header File
  - Scene and Config
- New Module and New Representation in the File menu now open wizards that show every file before it's created. The Module and Representation tiles of the New File sheet open the same wizards. (26A0134.012)
- The module wizard checks the name against all modules and representations, completes `REQUIRES`, `USES`, and `PROVIDES` from the repository, sorts the includes, and can create a parameter file for `LOADS_PARAMETERS`. (26A0134.013)
- The module wizard adds the provider to the `threads.cfg` of every scenario you check. Open files change through their document, so undo works, and if one write fails, nothing is kept. (26A0134.014)
- The representation wizard takes fields and an optional `.cpp` with `draw()`. It can continue into the module wizard, add `PROVIDES` to an existing module, or create the representation alone. (26A0134.015)
- A new file now regenerates the compile database, so clangd knows it at once. (26A0122.082)
- The File menu now contains Save (Command-S), Save All (Option-Command-S), and Close Tab (Command-W). (26A0122.083)
- A binary file now shows a message instead of unreadable text. (26A0122.084)
- The Project navigator now selects the file of the focused editor. (26A0122.255)
- You can now rename a file or folder in the Project navigator by pressing Return. The name is selected without its extension, and you can change the extension too. (26A0122.256)
- The context menu of the Project navigator now contains Show in Finder, Open in Terminal Tab, New File, New Folder, Rename, Duplicate, Move to Trash, Copy Path, and Copy Relative Path. Move to Trash asks first. (26A0122.257)
- The file menus now follow Xcode. (26A0122.258)
  - The Project navigator menu adds Open in New Tab, Open in Assistant, Open with External Editor, Copy #include Line, a Source Control submenu, and a B-Human section for the Module Graph, the Behavior Graph, Run in Canvas, and the config search path.
  - With several rows marked, the menu counts them: Move 3 Items to Trash, Copy 3 Paths, Stage 3 Files.
  - A folder has Find in Folder, Expand All, and Collapse All.
  - Generated configs show a lock, and Rename, Duplicate, and Move to Trash are dimmed with the reason.
  - Move to Trash (Command-Delete, or the Delete key in the navigator) names unsaved changes, bookmarks, and breakpoints that go with the files.
  - Right-click an editor tab for Close Other Tabs, Close Tabs to the Right, Show in Project Navigator, and more. Right-click a crumb of the jump bar for the same menu as in the navigator.
  - The Project navigator now lists files that were created, moved, or deleted in the Finder or a terminal.
  - A clean file that was deleted outside the editor now closes its tab. A file with unsaved changes keeps its tab, which shows "Deleted on disk", and saving writes it again.
- You can now move files and folders by dragging them in the Project navigator. A sheet lists what moves and offers multiple options: (26A0122.259)
  - Update #include lines, for the files that include a moved header
  - Generate the project afterwards
  - Move with git mv, which keeps the file history
  - Show Changes, which previews the changed `#include` lines
- Files you drag from the Finder into the Project navigator are now copied into that folder. (26A0122.260)
- Undo Move in the Edit menu now moves the files back. (26A0122.261)
- Dropping a file on an editor pane now opens it there. (26A0122.262)
- The Project navigator now hides the extension only for C, C++, Objective-C, Swift, and Metal files. (26A0122.263)
- `.ros3`, `.rsi3`, `.con`, and `.cfg` files now have their own icons in the Project navigator. (26A0122.264)
- The Project navigator now shows Xcode-like icons for files and folders. (26A0122.265)
- Scripts, source languages, logs, data files, and binaries now have their own icons in the Project navigator and in tabs. (26A0122.266)
- The new File Extensions setting in the General tab of Settings chooses to hide known extensions, hide all, or show all. The default is Hide Known. (26A0122.267)
- A `.onnx` file or a Keras `.h5` file now opens in a read-only neural network viewer. It draws the layers as blocks and shows the shapes. The inspector lists the files under `Src` and `Config` that use the network. (26A0122.268)
- You can now collapse the blocks of a network, collapse or expand all of them, scroll and zoom the view, and fuse Sigmoid and Mul to SiLU with Fuse Activations. (26A0122.269)
- The viewer reads only the structure of a Keras file, not its weights. (26A0122.270)
- A `.log` file now opens in a read-only log inspector. It shows the images of the log, plays them as video, and shows representations as tracks over a scrubber. You can export a frame as PNG, export all frames, and export a video. (26A0122.271)
- Log playback now follows a real-time clock, prefetches the next images, and skips frames when decoding falls behind, so 1x plays at 60 images per second in the log inspector and the Quick Look preview. (26A0122.272)
- YUYV images of a log are now converted with Accelerate and vImage, which takes under 0.1 ms instead of about 25 ms per image in Debug builds. (26A0122.273)
- The log inspector never writes the log. Open in SimRobot can change it, because SimRobot adds an index. (26A0122.274)
- The log inspector has a search field. Type a condition such as `theBallModel.seenPercentage == 0`, and the matching frames are marked on the timeline. (26A0134.016)
- A list shows each run of matching frames with its time range and length. Command-G and Shift-Command-G, or the arrow buttons, jump from run to run, and the image and values follow. (26A0134.017)
- Conditions use the type information stored in the log: field paths, comparisons, `&&`, `||`, `!`, `changed(x)`, and `in(x, a, b)`. An unknown name gets a "Did you mean" hint. (26A0134.018)
- Completion in the search field offers fields with their types and enum values. The search reads the Cognition thread by default, and a menu picks another thread. (26A0134.019)
- Sound files, images, and Markdown files now open in their own viewers. (26A0122.275)

#### Find

##### New Features

- You can now search the open file with Find (Command-F) and Find and Replace (Option-Command-F). Find Next, Find Previous, and Use Selection for Find are also available. (26A0122.086)
- The new Find in Project (Shift-Command-F) searches with `git grep`, groups the results by file, and has regex and case options. It stops at 2000 matches and says so. (26A0122.087)
- The Find navigator now has the scopes In Project, All Files, Project and Submodules, and Open File. All Files also searches untracked files. (26A0122.277)
- The new Find All References (Control-Shift-Command-F) groups the results by file and shows the line of each. (26A0122.088)
- While clangd indexes, the Find navigator now says that more references may appear, and the search runs again when indexing finishes. (26A0122.278)
- The new Find Call Hierarchy (Control-Shift-Command-H) in the Navigate menu and the context menu shows the callers of the function at the caret in the Find navigator. When clangd supports it, you can switch to Callees. (26A0122.279)
- The new Open Quickly (Shift-Command-O) finds files and symbols. An empty search shows your recent files. (26A0122.089)
- In Open Quickly, a trailing `:line` now jumps to that line, and Option-Return opens the result in Assistant. (26A0122.090)

##### Resolved Issues

- Fixed: Return in Open Quickly did not open the selected result, and the search did not remember its last query. (26A0122.280)

##### Known Issues

- No scope of Find in Project searches untracked files and submodules together. (26A0122.091)
- Find All References is incomplete until clangd finishes indexing. (26A0122.092)

#### Project Editor

##### New Features

- The new project editor opens from the project row at the top of the Project navigator. (26A0122.093)
- The project editor now shows different tabs for each selection: (26A0122.094)
  - Project: Info and Build Settings
  - App targets: General, Signing & Capabilities, Info, Resource Tags, Build Settings, Build Phases, and Build Rules
  - Library, tool, and test targets: General, Resource Tags, Build Settings, Build Phases, and Build Rules
  - Aggregate targets: Build Settings and Build Phases
- Changes now go to `Make/CMake/EditorOverrides.cmake`, and the project regenerates. It waits for a running build or deploy. (26A0122.095)
- If a change fails, the editor now rolls it back and shows a banner. (26A0122.096)
- The new General tab sets Minimum Deployments and edits Frameworks and Libraries, including their embed mode, and Development Assets. (26A0122.097)
- The new Signing tab sets automatic signing, the team, the bundle identifier, and the signing certificate. (26A0122.098)
- The new Build Settings tab contains multiple controls: (26A0122.099)
  - Basic, Customized, or All settings
  - Combined or Levels layout, where Levels has Resolved, Target, and Project columns
  - Names or Titles
  - Values or Definitions
  - A filter field
  - Add User-Defined Setting
- Setting cells now offer popups for booleans and enums, a reorderable list for paths, and one row for each configuration when values differ. (26A0122.100)
- The new Build Phases tab edits Target Dependencies and Compile Sources, with compiler flags for each file. (26A0122.101)
- You can now add Run Script phases, edit their script, and choose when they run. (26A0122.102)
- The new Build Rules tab lists the built-in rules. (26A0122.103)
- The target list now has a filter, and it becomes a popup when the window is narrow. (26A0122.104)

##### Known Issues

- Resource Tags is empty. (26A0122.105)
- You can't add or edit build rules. (26A0122.106)
- Link Binary With Libraries, Copy Bundle Resources, and copy phases are read-only. (26A0122.107)
- You can't remove or re-embed frameworks that come from CMake. (26A0122.108)
- Run Build Tool Plug-ins is always empty, and Supported Destinations always shows Mac. (26A0122.109)

#### Quick Look

##### New Features

- Space bar in Finder now shows robot logs, scenes, scene includes, console scripts, and B-Human configs with B-Editor's own viewers, and Finder icons show the field of a scene or a page of a file. (26A0122.281)
- `.ros2`, `.rsi2`, and `.rsi2d` files now get XML coloring, in the editor too. (26A0122.282)
- Space on an `.onnx` network shows its graph with a Layers tab, and space on a Keras `.h5` model shows its layer list with a Graph tab. Chips show the format, size, parameters, and layers, and a side column shows the inputs and outputs. Networks larger than 100 MB show only their format and size. (26A0134.020)
- Space on a `.cfg` file shows a read-only tree with a filter or the colored source. Files with nested values open as a tree, flat files as source, and the preview remembers your last choice. (26A0134.021)

##### Known Issues

- Finder keeps the text thumbnail of macOS for robot logs. (26A0122.283)

  **Workaround:** Use the preview. Press the space bar.

#### Scene Editor

##### New Features

- `.ros3` scenes now open in the new scene editor, with Field, Source, and Split modes. (26A0122.284)
- The field now comes from the `fieldDimensions.cfg` of the location of the scene, or of Default. (26A0122.285)
- You can now drag robots and the ball on the field, and turn a robot with its rotation handle. Each drag is one step for Undo. (26A0122.286)
- The arrow keys now move the selected robot or the ball by 100 mm, and Delete removes the selected robot. (26A0122.287)
- The bar above the field now changes the location and the scenario of the scene, and Add Robot adds a robot to a team. (26A0122.288)
- The Document inspector now edits the name, type, position, rotation, team, color, and player number of the selected robot, and the position of the ball. (26A0122.289)
- Changing the color of a team now also updates the `TeamColor` of its robots. (26A0122.290)
- Robots from included `.rsi3` files now appear dimmed on the field. Show in Source in the inspector opens the include. (26A0122.291)
- The new Library (Shift-Command-L) in the toolbar contains a robot for each team, a dummy, and the ball. Drag an item onto the field, or double-click it to add it at the center. Hold Option while you drop a robot to make it the goalkeeper. (26A0122.292)
- You can now zoom the field with a pinch or with the zoom buttons, from 25 to 400 percent. (26A0122.293)
- Split mode now shows the field next to the source, and an edit on one side appears on the other at once. Changed values are marked for a moment. (26A0122.294)
- When SimRobot runs the open scene, the new Restart on Save switch restarts it after you save the scene, its `.con` file, or one of its includes. (26A0122.295)
- The new Manage Scenes in the Product menu lists every scene with its location, scenario, field, and robots. (26A0122.296)
- New Scene in Manage Scenes now creates an empty K1 or T1 scene, or a copy of another scene and its `.con` file. (26A0122.297)

##### Known Issues

- Robots defined in an include can't be moved in the scene editor. (26A0122.298)

  **Workaround:** Choose Show in Source in the inspector and edit the include.

- Dummies can't be selected or moved on the field. (26A0122.299)

  **Workaround:** Edit their position in Source or Split mode.

#### Settings

##### New Features

- The new Settings window contains tabs for General, Themes, Text Editing, Key Bindings, Source Control, Behaviors, Discord, Locations, and Updates. (26A0122.110)
- The new General tab sets the appearance to System, Light, or Dark, and controls reopening files, saving before a build, and generating the project before a build. (26A0122.111)
- The new Themes tab reads the themes of Xcode and your own themes from Xcode's folder. You can choose one theme for light and one for dark appearance. (26A0122.112)
- You can now add a theme and change the color of each token. Editing a built-in theme creates a Customized copy. (26A0122.113)
- The Themes tab also sets the font, the editor and console font size, and the line spacing. (26A0122.114)
- The new Text Editing tab contains multiple options: (26A0122.115)
  - Line numbers, minimap, and page guide with its column
  - Wrap lines and hanging indent
  - Spaces, tab width, and indent width
  - Auto-close brackets and suggest completions while typing
  - Trim trailing whitespace and format with bstyle on save
  - Parameter and type hints
- The new Key Bindings tab records shortcuts and warns about conflicts. You can clear a binding, restore its default, and search by command, menu, or key. (26A0122.116)
- The new Behaviors tab chooses what happens when a build starts or fails, when a run starts or pauses, and when a deploy starts. (26A0122.117)
- The new Source Control tab sets the status badges and the refresh on activation, and it shows your Git name and email. (26A0122.118)
- The new Locations tab chooses the repository without a restart, and the open workspace follows. (26A0122.119)
- The Locations tab also shows the build products in the Finder, shows and clears the size of the compile database, and shows the state of clangd and lldb-dap. (26A0122.120)
- The General tab of Settings now has a File Extensions choice. See Files. (26A0122.300)
- The Behaviors tab now sets how a saved module is patched in the canvas: automatically, manually, or off. See Simulation. (26A0122.301)
- The Behaviors tab now has a Canvas section. It turns the refresh on save on or off. (26A0122.302)
- The new Discord tab turns the Discord activity on or off and sets what it shares. See General. (26A0122.303)
- The new setting Warn about unused includes shows the clangd unused-include warnings. It is off by default, so a file no longer fills the Issues navigator with them. (26A0134.022)
- The new Simulator tab applies the simulation patch package to your checkout. Choose the zip, see whether it applies to your checkout and how far HEAD is from the commit it is based on, and click Apply. Remove takes exactly these changes out again. Nothing is committed, pushed, or merged. See Simulation. (26A0134.023)
- The Simulator tab keeps a copy of the package, so Remove works after the zip is gone. Update chooses a package for a new master. (26A0134.024)

##### Known Issues

- The dark theme colors aren't matched to Xcode yet. (26A0122.121)
- You can't rename a custom theme. (26A0122.122)
- The When column in Key Bindings always reads Always. (26A0122.123)
- The preset menu in Key Bindings contains only Xcode Default. (26A0122.124)
- You can't change the shortcuts for Undo and Redo. (26A0122.125)

#### Simulation

##### New Features

- The new Canvas runs a scene next to the code, in a separate SimRobotHost process without Qt. You open it with Canvas in the Editor menu (Option-Command-Return) or with the Canvas button in the toolbar. (26A0122.304)
- The Canvas button sits in the middle group of the toolbar, together with Assistant and Code Review, as in Xcode 27. The old standard editor button is gone. (26A0122.305)
- Run now starts the scene in the canvas when the canvas is shown. Otherwise Run starts `SimRobot.app` as before. (26A0122.306)
- The canvas runs under `lldb`, so breakpoints, the Debug navigator, and the variables pane work with the simulation. (26A0122.307)
- The canvas builds only the `SimRobotHost` target, and it doesn't run `Make/macOS/generate`. In a linked Git worktree, the editor asks once before it runs generate. (26A0122.308)
- The control bar above the picture contains the simulation controls, a robot popup, and a game state popup. It adapts to the width of the canvas in three steps. (26A0122.309)
- The SimRobot tab now shows the console of the host with an input line, history, and Tab completion of console commands. (26A0122.310)
- A repository without the SimRobotHost target now shows Simulation Not Available in the canvas. The message says that the simulation needs the simulation patch package. (26A0122.311)
- The simulation patch package contains the changes to B-Human and to `Util/SimRobot` as two patches, a manifest, `apply.sh`, and `revert.sh`. `apply.sh` checks first and then changes only the files of your checkout, and `revert.sh` removes exactly what it applied. The package works on the B-Human commit named in its file name. Revert it before you pull, and apply the package for the new master afterwards. (26A0134.025)
- Debug views in the canvas have six tabs: Scene, Image, Field, Behavior, Timing, and Data. (26A0122.312)
  - Scene shows the 3D picture of the scene.
  - Image shows the camera picture with its drawings. The Drawings popover has one row for each drawing of the robot and Hide All Drawings.
  - Field shows the world state on the field.
  - Behavior shows the option table with the current option and state.
  - Timing shows the duration of each module in a sortable table.
  - Data shows a representation as a read-only tree.
- In Image and Field, drag to pan, pinch to zoom, and double-click to show everything. (26A0122.313)
- When you save a C++ file, the canvas now rebuilds `SimRobotHost` in the background. The old simulation keeps running at background priority during the build. (26A0122.314)
- After the build, the editor hands the robots, the ball, the game state, the camera, and the pacing over to a new host that starts next to the old one. The canvas switches on the first frame of the new host. (26A0122.315)
- The debugger attaches to the new host after the switch, which takes about 3 seconds. (26A0122.316)
- A refresh took 17 to 25 seconds from save to new code with K1/Game. The SimRobot console shows a timing line for each refresh. (26A0122.317)
- Saving a `.cfg` file hands the state over without a build. Saving the `.ros3` or `.con` file of the running scene restarts the host. (26A0122.318)
- Debug views now continue across the hand-over. (26A0122.319)
- Saving a change inside one module now compiles that module into a bundle and swaps it into all robots at their next frame, without a restart. A module with one file took about 3 seconds, and an option change in SkillBehaviorControl took 4.1 to 4.6 seconds. Options keep their state and state time. An option whose state no longer exists in the new code restarts in its initial state. (26A0122.320)
- A change that the editor can't swap shows the reason and uses the rebuild path. Examples are a header that many modules include, a change in two modules, and a change of a `.cfg` file together with code. (26A0122.321)
- The Live Modules popover lists the patched modules. Revert to Built returns a module to the built code, and Rebuild All starts an ordinary refresh. (26A0122.322)
- In the manual mode, the pill shows the collected changes with Patch Now. The `patch` command in the SimRobot tab does the same. (26A0122.323)
- While the debugger holds the simulation, the pill shows Patch waits for Continue, and the patch starts on Continue. (26A0122.324)
- A pill, a toast, and lines in the SimRobot tab now show the progress and the time of each patch. (26A0122.325)
- A patch that fails to compile now sends its errors to the Issues navigator, and the old code keeps running. (26A0122.326)
- When you hide the canvas, the simulation now pauses, stops, or keeps running, as set in When the Canvas Is Hidden in the control bar's menu or in Settings. With live patches, Stop the Simulation pauses instead and says why. (26A0122.327)
- The Behavior tab now has the modes Table, Graph, and History, and a robot picker. (26A0122.328)
- Graph mode draws the running CABSL option as a graph of its states and transitions, and it lights the current state of the robot with its state time. (26A0122.329)
- Graph mode marks the transition the option just took, and a path above the graph lists the options from the root to the deepest one. (26A0122.330)
- History mode lists the transitions of the picked robot from the last 10 minutes, as a list or a timeline, and a filter limits it to one option. In scenes that request the activation graph, such as the standard game scenes, the history starts when the simulation starts, not when you open the tab. (26A0122.331)
- A row in History opens the graph of that transition with its source line, and Open Graph and Open Source jump to the option. (26A0122.332)
- While the Behavior tab of the canvas is open, the CABSL graph in an editor tab now shows "Live from robotN" and lights the state of the running option. (26A0122.333)
- A hot swap of behavior code now reports whether the behavior was kept and which options restarted, in a toast, a card, the Live Modules popover, and the SimRobot tab. The behavior is kept across the swap, and the report lists the options that restarted. (26A0122.334)
- Hot swap now works for module folders with several modules, such as BallStateEstimator and FieldPerceptors, and one save patches all of their modules. (26A0122.335)
- Revert to Built now reverts all modules of a folder together, or none. (26A0122.336)
- The simulation host now runs at background priority while a patch compiles and links. (26A0122.337)
- Under the debugger, loading a patch bundle can take long because lldb stops the process for each loaded image, so the editor now waits for the host to start the swap and then up to 180 seconds, instead of failing after 30 seconds. (26A0122.338)
- A patch or revert that times out no longer leaves the Live Modules list wrong, because the late answer of the host now updates it. (26A0122.339)
- Revert to Built now falls back to a rebuild when the host does not answer. (26A0122.340)
- A swap that takes long now says in the SimRobot console where the time went. (26A0122.341)
- Revert to Built now shows "Reverting" with the module's name until the host answers, and the Revert buttons are disabled meanwhile. (26A0122.342)
- The canvas now stays current when the editor is busy: updates that arrive while the main thread is occupied are merged into one batch, so a heavy layout or a busy Mac no longer builds an ever-growing backlog of stale states and frames. (26A0122.343)
- Hot swap answers are now handled first in each batch, so a patch or Revert to Built no longer waits behind queued view updates. (26A0122.344)
- The merge never drops console lines or behavior transitions, so the behavior history stays complete. (26A0122.345)
- Restarts of options with variables now show as a quiet group in the toast, the card, the Live Modules popover, and the SimRobot console, and only other restarts are warnings. (26A0122.346)
- The patch builder now rebuilds its precompiled header when a header it includes changed, for example Module.h, and tries once more if clang reports a stale header. (26A0122.347)
- The canvas control bar now has a Stop button. It asks first only when live patches would be lost, and "Ask before stopping with live patches" in Settings turns the question off. (26A0134.026)
- After a stop, the canvas shows which scene ended and when, how many live patches were not kept, and a Run button. (26A0134.027)
- Revert to Built now asks whether to discard the code changes too. Simulation Only keeps the edited files. Simulation and Code restores them as one undo step, and the toast offers Undo. "Don't ask again" stores the answer in Settings. (26A0134.028)
- The simulation canvas has a new Plot tab. Plots that a script declares with `vp` and `vpd`, such as JointTorque, Walk, and Whistle, are drawn as live graphs. The tab appears only while the robot has a plot view, and a popup picks the plot by name. (26A0134.029)
- A plot shows a line for each layer, a legend with the newest value, y labels with units, and the time span. Hovering shows a cursor with the values at that sample. (26A0134.030)
- The range of a plot comes from `vp`. Autoscale fits it to the values, and values outside the range are pinned to the edge and marked. (26A0134.031)
- Pause freezes a plot while new values keep arriving, and Copy Values copies the visible series as tab-separated text. A plot whose data can't be read says why. (26A0134.032)
- While a simulation runs, resting the pointer on a representation or a member in module code shows its live value for the chosen robot, with child rows for records, a pin button, Pin to the Inspector, and Plot. Values update up to 10 times a second. While the debugger is paused, its data tip shows instead. (26A0134.033)
- The Data tab is now the Representation Inspector. It has robot and representation pickers with the provider module and Show Header, a filter, Pause, a tree with sparklines of the last 10 seconds, and a Pinned section for values of several representations. (26A0134.034)
- The row menu of the Representation Inspector offers Pin to Plot, Show in Plot Tab, Show Declaration, Find Uses in Code, Copy Path, and Copy Value. Pinning to the plot opens a resizable plot drawer under the tree, which can pop out into its own window. (26A0134.035)
- Show in Inspector in the Navigate menu (Control-Option-Command-D) opens the Representation Inspector on the representation at the caret. (26A0134.036)
- The new Live Values setting chooses Hover Only, Inline for Pinned, which shows pinned values at the end of their code lines, or Off. Image-sized types such as `CameraImage` and `LinePercept` show no value. (26A0134.037)

##### Resolved Issues

- Fixed: The patch called a module of SkillBehaviorControl "new" when you saved it. (26A0122.348)
- Fixed: A module with an ONNX network did not link or patch. (26A0122.349)
- Fixed: The Drawings popover did not show a new drawing right after a patch. (26A0122.350)
- Fixed: A stale `saveState` timer could end a later save. (26A0122.351)
- Fixed: A late answer of the host could complete the next patch or revert request. Requests now carry an id, and the editor drops an answer with another id. (26A0122.352)
- Fixed: The 30 s timeout of a patch could end a later request. It now ends only the request it was started for. (26A0122.353)

##### Known Issues

- With cameras for 10 robots, the simulation runs at about 0.4 of real time, because the perception of the robots saturates the CPU. Scenes with a percept oracle, such as K1/GamePerceptOracle, run in real time. (26A0122.354)

  **Workaround:** Use a Percept Oracle scene.

- Each patch slows the simulation for a few seconds, down to 0.09 of real time. (26A0122.355)

- A refresh takes 17 to 25 seconds from save to new code. (26A0122.356)

  **Workaround:** Set hot swap to automatic, so a change inside one module takes about 3 to 5 seconds.

- Swapping a whole thread at once isn't proven stable. (26A0122.357)

- After several rebuilds, the restored game state can differ from the game before, because the score, the half, and the remaining time are not carried over. (26A0122.358)

- Options with option variables, such as Zweikampf, GoToBallAndKick, and WalkToBallAndKick, restart in their initial state after a hot swap, because their variables are not carried yet. (26A0122.359)

- Hot swap doesn't work in log replay yet. (26A0122.360)

- The scale of the zoom gesture in the canvas is unverified with a real mouse. (26A0122.361)

#### Source Control

##### New Features

- The new Source Control navigator lists uncommitted changes with a filter, and the Project navigator shows status badges. (26A0122.127)
- The Source Control navigator now groups files into Merge Conflicts, Staged Changes, and Uncommitted Changes. Each file has a button to stage or unstage it, and Stage All and Unstage All act on a whole group. (26A0122.362)
- You can now commit from the Source Control navigator. Enter a message and click Commit, or select Amend to change the last commit. Commit (Option-Command-C) in the Integrate menu moves the focus to the message. (26A0122.363)
- The new Repositories mode lists the current branch, local branches, remotes with their branches, and tags. (26A0122.128)
- The new Code Review mode shows the `git diff` of a file. (26A0122.129)
- Code Review now shows a file side by side. You can stage, unstage, or discard the whole file or a single change. (26A0122.364)
- The History inspector now lists up to 100 commits of a file, following renames. Click a commit for Show Commit and Open in Code Review. (26A0122.365)
- Click the branch in the debug bar to open the new branch list, with a Find field and the current, local, and remote branches. Click a branch to switch to it. A remote branch gets a local tracking branch. (26A0122.366)
- The new Create Branch sheet in the Integrate menu and the branch list creates a branch from a base branch and switches to it. (26A0122.367)
- The Integrate menu now contains Pull (Option-Command-X), Push (Option-Command-P), Fetch Changes, Refresh File Status, and Switch Branch. Pull also updates the submodules. (26A0122.368)
- Push now asks first when the branch has no upstream, and then creates it on the remote. (26A0122.369)
- When a pull changes files under `Make/CMake`, B-Editor now offers Generate Project. (26A0122.370)
- The new merge editor shows each file with a conflict, with Local and Remote side by side. Choose Use Left, Use Right, or both in either order for each conflict, then click Mark as Resolved. (26A0122.371)
- The merge editor also resolves binary, deleted, and submodule conflicts, and Abort Merge ends a merge or a rebase after a confirmation. (26A0122.372)
- When no conflicts remain, Commit in the Source Control navigator now creates the merge commit with the message from Git. (26A0122.373)
- When a pull ends in conflicts, the merge editor now opens the first file, and an alert lists the files and offers Open Source Control. (26A0122.374)
- Git status now refreshes when you return to the app. You can turn this off in Settings. (26A0122.130)
- Changed lines now have bars in the gutter and marks in the minimap: green for added lines, blue for changed lines, and a red wedge where lines were deleted since the last commit. Click a bar to see the old text, revert that change as one undo step, or copy the old text. "Show changes since the last commit" in Settings > Source Control turns them off. (26A0134.038)
- Every save that changes a file now keeps a local version in Application Support, never in the repository. Unnamed versions are kept for 7 days, with at most 100 for each file and 200 MB in total. Named versions never expire. (26A0134.039)
- B-Editor also keeps the previous text when a git checkout or pull, bstyle, or Revert to Built with code replaces an open file. (26A0134.040)
- The new Local History in the Editor menu lists the versions of a file by day and compares a version with the current file or with another version. You can restore a whole version or a single change, each as one undo step, and name a version. The History inspector shows the same versions in its Local segment. (26A0134.041)
- The branch in the toolbar now follows a change of HEAD that you make in the Terminal tab or in another tool. (26A0134.042)

##### Resolved Issues

- Fixed: Committing or marking a conflict resolved could fail with "Unable to create index.lock" when the background refresh of the editor ran `git status` at the same moment. Git reads now run with `--no-optional-locks`. (26A0122.375)

##### Known Issues

- The merge editor can't continue a rebase. (26A0122.376)

  **Workaround:** Run `git rebase --continue` in the Terminal tab.

- Pull and Push run at once with the settings of Git. No dialog lets you choose a remote, a branch, or a rebase. (26A0122.377)

#### Source Editor

##### New Features

- The new source editor uses clangd for C, C++, Objective-C, and Objective-C++, with completion, hover, semantic colors, and live issues. (26A0122.134)
- The toolbar now shows clangd Not Running when clangd fails to start or exits repeatedly. Click it to open the Locations tab of Settings. Rename then says that clangd isn't running. (26A0122.378)
- `.cfg` files and shell scripts now have syntax colors. A file without an extension counts as a shell script when it starts with a shell shebang. (26A0122.135)
- `.ros3` and `.rsi3` scenes and `.con` console scripts now have syntax colors. (26A0122.379)
- Completion now opens after `.`, `->`, `::`, and two typed letters, or with Show Completions (Control-Space). (26A0122.136)
- The completion list now ranks exact matches first and shows the kind, return type, signature, and documentation of each item. (26A0122.137)
- Completion now knows the B-Human macros, and it adds `()` to functions. (26A0122.138)
- The new macro completion contains multiple features: (26A0122.139)
  - `REQUIRES`, `USES`, `PROVIDES`, and `PROVIDES_WITHOUT_MODIFY` offer representations and add their `#include` next to the other representation includes.
  - `DEFINES_PARAMETERS` and `LOADS_PARAMETERS` insert their block.
  - `STREAMABLE` and parameter macros offer built-in and project types.
- In `.con` files, completion now offers the SimRobot console commands from `Src/Libs/SimulatedRobot/Commands`, their argument words, the scripts for `call`, and the robot names of the scene. (26A0122.380)
- Option-click on a console command now shows its usage, scope, and declaration in Quick Help. (26A0122.381)
- `.con` files now show a warning for an unknown command. (26A0122.382)
- The new inlay hints show parameter names and deduced types. (26A0122.140)
- Inlay hints now name the arguments of function-like macros with two or more parameters. Arguments inside `STREAMABLE`, `STREAMABLE_WITH_BASE`, `DEFINES_PARAMETERS`, and `LOADS_PARAMETERS` get no parameter hints. (26A0122.383)
- You can now highlight every use of a symbol with Option-click, which also opens Quick Help. (26A0122.141)
- Holding Command or Option now outlines the symbol under the pointer. Command-click jumps to its definition. (26A0122.384)
- Quick Help now opens in a popover next to the symbol. (26A0122.385)
- The new Quick Help shows which module provides a representation, which modules require and use it, and which threads and scenarios assign each provider. (26A0122.142)
- The Document inspector now shows the Provides, Requires, Uses, and Parameters of a module, and the threads and scenarios that run it. (26A0122.143)
- For a module, the Document inspector also lists its drawings, plots, debug responses, and modify IDs, each with a SimRobot command you can copy. (26A0122.386)
- For a representation, the Document inspector now shows its fields and the modules that provide and require it. (26A0122.387)
- Jump to Definition (Control-Command-J or Command-click), Find All References, Rename, Open Quickly, and Find in Project are now available. (26A0122.144)
- The new Rename command checks the new name and previews every changed line by file. It also changes closed files, undoes a failed write, and warns when `.cfg` files use the name. (26A0122.145)
- The Rename preview now looks like Xcode's. It shows each file with the lines that change and two lines of context in the colors of the editor, and the new name appears in all lines while you type. (26A0134.043)
- The tabs All, Code, Comments, and Strings filter the preview and show how many places each has. A checkbox for each file takes it out of the rename, and a chevron folds it. The panel and the folds animate, unless Reduce Motion is on. (26A0134.044)
- The note about `.cfg` files that use the name is now one line above the list. Show opens the files in a short list, so a name used in dozens of configs no longer pushes the code out of view. (26A0134.045)
- Rename now works on a field that you declare as a macro argument, such as `lastPerception` in `STREAMABLE`. clangd has no symbol at such a declaration, so the editor asks clangd from a use of the name, accepts it only when its references contain your declaration, and adds the declaration if the edits lack it. Another field with the same name is never taken. (26A0134.046)
- The new Edit All in Scope (Control-Command-E) edits every use of a symbol in the file at once, or in its function for a local name. Press Escape to finish. (26A0122.388)
- The new context menu contains Jump to Definition, Find All References, Rename, Show Quick Help, and the clipboard commands. (26A0122.146)
- The new Show Code Actions (Shift-Command-A) in the Editor menu and the context menu lists the quick fixes and refactorings of clangd at the caret. (26A0122.389)
- Signature help now appears when you type `(` or `,` in a call. It shows the active parameter in bold with its documentation, and Control-Up and Control-Down switch between overloads. (26A0122.390)
- You can now fold braces and block comments in C and C++ files. Click the ribbon next to the line numbers, or choose Fold (Option-Command-Left), Unfold (Option-Command-Right), Fold All, or Unfold All in the Editor menu. Click a folded block to open it. (26A0122.391)
- The new sticky headers keep up to 3 enclosing function and block headers at the top of the editor while you scroll. Click one to jump to it. You can turn them off in Settings. (26A0122.392)
- You can now add a caret with Control-Shift-click, or above and below with Control-Shift-Up and Control-Shift-Down. Option-drag adds a caret on each line. Press Escape to return to one caret. (26A0122.393)
- Select Next Occurrence (Option-Command-E) and Select All Occurrences in the Find menu now select the matches of the selected word, so you can edit them together. (26A0122.394)
- Return now indents in Allman style for braces, labels, templates, initializer lists, and bodies without braces. (26A0122.147)
- Return now continues a block comment, and `/**` adds its closing line. (26A0122.148)
- Typing `{`, `}`, `#`, or a `case` or access label now indents the line. (26A0122.149)
- Brackets and quotes now close automatically, and you can type over the closing character. (26A0122.150)
- Delete in an empty pair of brackets or quotes now removes both characters. (26A0122.395)
- The new Editor menu contains multiple commands: (26A0122.151)
  - Re-Indent (Control-I)
  - Move Line Up (Option-Command-Left Bracket) and Move Line Down (Option-Command-Right Bracket)
  - Shift Left (Command-Left Bracket) and Shift Right (Command-Right Bracket)
  - Comment Selection (Command-/)
  - Add Documentation (Option-Command-/), which inserts a stub with `@param` and `@return`
- Comment Selection now uses `#` in shell scripts and `.con` files, and `<!-- -->` in `.ros3` and `.rsi3` files. (26A0122.396)
- The new Format File (Control-Shift-I) in the Editor menu formats a C, C++, or Objective-C file with bstyle, also with unsaved changes. (26A0122.397)
- Tab and Shift-Tab now indent and outdent a selection of lines. (26A0122.152)
- Control-J now joins lines, Control-Left and Control-Right move by subword, and Command-Delete deletes to the start of the line. (26A0122.153)
- The new Functions in File command (Control-6) lists the functions and declarations of the file, and Jump to Line (Command-L) opens a line. (26A0122.154)
- Switch to Header and Switch to Source (Control-Command-Up and Control-Command-Down) now open the counterpart file. (26A0122.155)
- The new gutter shows line numbers, issue icons, and breakpoints. (26A0122.156)
- You can now add or remove a bookmark on the current line with Add or Remove Bookmark (Control-Shift-Command-B) in the Editor menu. Bookmarks appear in the gutter, move with your edits, follow renamed files, and persist for each repository. (26A0122.398)
- The Bookmarks navigator now lists your bookmarks by file with their line. Click one to open it, or press Delete to remove it. (26A0122.399)
- The new Authors item in the Editor menu shows the author, date, and commit of each group of lines next to the editor. Click a group to see the commit message, with Show Commit and Copy Hash. (26A0122.400)
- Issues now appear at the end of their line. A Fix button applies the fix from clangd. (26A0122.157)
- The new minimap (Control-Shift-Command-M) shows the file and scrolls it when you click or drag. (26A0122.158)
- The new Wrap Lines (Control-Shift-Command-L) wraps long lines, and wrapped lines hang under their indent. (26A0122.159)
- Increase Font Size, Decrease Font Size, and Reset Font Size now change the editor font. (26A0122.160)
- Documentation comments now use a prose font. (26A0122.161)
- Shell scripts are now checked while you type with `bash -n`, `sh -n`, or `zsh -n`, depending on the script. (26A0122.162)
- Saving now trims trailing whitespace on the lines you edited. The new Trim trailing whitespace on save choice in the Text Editing tab of Settings also offers Current File, Current File and Blank Lines at End, and Don't Trim. (26A0122.163)
- Saving can now format C and C++ files with bstyle. This is off by default. (26A0122.164)
- Editor Only (Command-Return), Assistant (Control-Option-Command-Return), and Code Review (Option-Shift-Command-Return) are now in the Editor menu and the toolbar. (26A0122.165)
- The new Assistant mode shows the counterpart of the open file next to it, such as a header next to its source file. (26A0122.166)
- A `.cpp` file under `Src/Modules/BehaviorControl` with CABSL options now opens as a graph of the states and transitions of each option, with a switch to Source. Double-click a state to jump to its code. (26A0122.401)
- The new Behavior Overview in the Navigate menu shows the root option of a scenario with its options in priority order, and the options each of them calls. (26A0122.402)
- The compile database now builds in a cache folder and updates when `Make/CMake` or the list of source files changes. (26A0122.167)
- clangd now restarts after a crash, up to 5 times a minute. (26A0122.168)
- Completion in `.con` scripts now suggests argument values: debug requests after `dr`, representations and modules after `mr`, and drawings, plots, and images after `vfd`, `vid`, `vpd`, `vi`, and `get`. Names the running simulation reports come first and are tagged Simulation. Names read from the sources follow and are tagged Code. (26A0134.047)
- Without a running simulation, the completion popup of a `.con` script says so and offers Run. (26A0134.048)
- Every completion popup now matches the start of a name, the start of a part after `:`, camel-case initials such as `RFC`, and letters in order such as `rlfc`. Matched letters are bold. C++ completion keeps the fuzzy results of clangd. (26A0134.049)
- In the completion popup, the arrow keys show the syntax of the command with the current argument marked, and what is known about the selected name. (26A0134.050)
- Console scripts show predictions as grey text after the caret. Tab, or Right Arrow at the end of the line, accepts them, and Esc dismisses them. While a prediction shows, the completion popup stays closed; Control-Space opens it. Predictions come from the scripts of the project and the names of the running robots or of the code. A setting in Text Editing turns them off. (26A0134.051)
- While the simulation runs, violet markers in the gutter show the lines that differ from the built code. A filled dot means the robots run the line. A ring means they don't, for example after Revert to Built, after a failed patch, or before the patch arrives. (26A0134.052)
- Lines that run live get a faint violet background. "Live line background" in Settings turns it off. (26A0134.053)
- Hovering a marker shows since when the line runs, in which patch, and on how many robots. Clicking it offers Show Diff to Built Code, Discard This Change, Discard All Changes in This File, and Revert to Built. (26A0134.054)
- Files with live changes get a violet dot on their editor tab and in the Project navigator, and the minimap marks the changed lines. (26A0134.055)
- Brackets in C and C++ files get a color for each nesting level. A bracket without a partner is red with a wavy underline. (26A0134.056)
- With the caret next to a bracket, both brackets of the pair get a soft box, also across lines. (26A0134.057)
- Thin vertical scope lines show each `{ }` block, and the block around the caret is stronger. (26A0134.058)
- The new Brackets and Scope sections in Settings > Text Editing turn bracket colors, the matching pair, and scope lines on and off. All are on by default. (26A0134.059)
- In a module header, a `REQUIRES` or `USES` line now gets a warning when no module provides the representation in the thread of a scenario that runs the module. Clicking the marker offers adding the provider to `threads.cfg`, changing `REQUIRES` to `USES`, removing the line, or showing the module in the Module Graph. (26A0134.060)
- A representation that one other thread provides shows an info marker at its line. A representation that several other threads provide is an error. (26A0134.061)
- TODO and FIXME in comments are now bold and amber. Settings > Notes adds more keywords. (26A0134.062)
- Option-drag now selects a rectangle with the same columns on every row and shows its size. Shift-Option-Up and Shift-Option-Down change the rows, typing replaces the text on all rows, and a row that is too short gets a caret at its end. (26A0134.063)
- Control-Option-Up grows the selection by syntax node from clangd, and Control-Option-Down shrinks it again. Without clangd, and in `.cfg` and `.con` files, the selection grows by word, string, brackets, and line. (26A0134.064)
- A block of two or more lines pasted into a code file now takes the indent of the line it lands on. The first Command-Z restores the block as copied, and Option-Shift-Command-V pastes it exactly as copied. (26A0134.065)
- The new Selection and Editing section in Settings > Text Editing turns rectangular selection, Edit All in Scope, expand and shrink selection, and smart paste on and off. A feature that is off also disables its menu item and key. (26A0134.066)
- A 16-point ruler next to the minimap now marks the whole file: errors and warnings, find matches, and live-patch lines each have their own lane, and a gray box shows the visible part. It stays when the minimap is hidden. (26A0134.067)
- Hovering a mark in the ruler shows its line, kind, and message. Clicking a mark moves the caret to its line, and Option-clicking goes to the next mark nearby. (26A0134.068)
- The find lane fills while the find bar is open or a word is highlighted. (26A0134.069)
- The new Scroll Bar section in Settings > Text Editing turns the ruler and each kind of mark on and off. (26A0134.070)
- Code completion now offers snippets with a gray S badge: MODULE, STREAMABLE, and the CABSL option, state, init, and trans in behavior files, a parameter line, and for, foreach, if, ifelse, while, switch, lambda, and class. Tab and Shift-Tab move between the fields, a field that appears twice changes in both places, and Esc ends the snippet. Inserting a snippet is one undo step. (26A0134.071)
- The new Snippets tab in Settings lists the B-Human, General, and your own snippets. You can create, duplicate, delete, import (`.json` and Xcode `.codesnippet`), and export snippets. Your own snippets are stored in Application Support, never in a repository. (26A0134.072)
- Comments, strings, `.cfg` and `.con` comments, and Markdown and text files are now spell-checked with a dotted underline. Code, Doxygen tags, paths, and format strings are never checked. (26A0134.073)
- Control-click a marked word for suggestions, Learn Spelling for Me, Learn Spelling for This Repository, and Ignore Spelling. Learned words are stored in Application Support, never in a repository. English (US) and German can be checked together, and the switches are in Settings > Text Editing. (26A0134.074)
- The new Command Palette (Shift-Command-P) lists every menu command and toggle with its shortcut. Initials such as "cp" match, your last 10 commands come first, a dimmed command says why it can't run, and toggles show On or Off. (26A0134.075)
- The new Clipboard History (Shift-Command-V) keeps your last 50 copies from the editor and its terminals, with search, a preview, and pins. Option-Return pastes an item with the indent of the caret line. The history lives only in memory and skips items that password managers mark as private. (26A0134.076)
- Compare With in the Editor menu shows the current file side by side with the clipboard, another file, or its header or source, like Code Review. Use Clipboard Lines takes a change into the open file as one undo step. Control-Option-Command-C compares the selection with the clipboard. (26A0134.077)
- Resting the pointer on a `Vector2f` or `Pose2f` in C++ or in a `.cfg` file now shows where it is on the field: a point, a pose with an arrow, or all entries of a list with the hovered one in red. Robot-relative values such as `ballOffset` show a grid around the robot. (26A0134.078)
- The field preview evaluates literals, `_deg` and `_rad`, `pi`, `theFieldDimensions` members, and simple arithmetic. It shows nothing for function calls and variables. (26A0134.079)
- The field preview uses the location of the selected target. A Location menu shows another field, and a Field/Robot switch is remembered for each member. (26A0134.080)
- When you pin the field preview, you can drag a point or an arrow to change the literal in the source as one undo step, and show a second field beside the first. A value outside the field is drawn at the edge with a warning. (26A0134.081)
- The `.cfg` table shows the same field preview when you rest the pointer on a row. "Show a field preview on hover" in Settings > Text Editing turns it off. (26A0134.082)
- In a module header, each `LOADS_PARAMETERS` member now shows the value that the `.cfg` of the selected target gives it. A dot marks a value that other scenarios resolve differently, and "no value" marks a key that no loaded file has. (26A0134.083)
- Clicking a value shows the search order with the file that wins and the values of the other scenarios. You can change the value there, which is one undo step when the file is open, add a missing entry, or open the table, the source, or Override In. Resting the pointer on a parameter in the module's `.cpp` shows the same card. (26A0134.084)
- Degree literals such as `90_deg` and `45deg` now show their value in radians, and `pi`, `pi_2`, `pi_4`, `pi2`, and plain numbers of `Angle` keys in `.cfg` files show degrees. Zero and plain numbers stay unmarked. (26A0134.085)
- The Inlay Hints section in Settings > Text Editing has the new Config Values and Angle Values settings and a precision for radians. (26A0134.086)
- Rename on a representation name or `theX` now opens Rename Representation instead of refusing. It renames the type, every `theX`, the `REQUIRES`, `USES`, `PROVIDES`, and `MODIFIES` arguments, `representation = X` in every `threads.cfg`, `.cfg` values, and the representation in `.con` scripts. Each group has a checkbox, and a preview shows the change of the selected line. (26A0134.087)
- Rename Representation can also rename `X.h` and `X.cpp` with `git mv` and fix the include lines. Comments that mention the name are listed but unchecked. If any part fails, every file written is restored. (26A0134.088)
- Rename Representation is also available in the Representations list and in the Module Graph. (26A0134.089)
- A gray line above functions, classes, structs, modules, and `STREAMABLE` types now shows how many places use them, how many functions call a function, and how many types derive from a type. Clicking a count opens the list, and Return jumps to the selected place. (26A0134.090)
- Show Call Hierarchy in the Navigate menu (Option-Control-Command-H) opens the callers and callees of a function in a popover. The arrow keys move, Right Arrow opens up to three levels, Space shows the call, and Return jumps to it. (26A0134.091)
- Show Type Hierarchy in the Navigate menu (Option-Control-Command-Y) shows the bases, the type, and the derived types in a popover. A base that `MODULE` generates is marked, and long lists show the first 30 rows. (26A0134.092)
- The new Code Lens section in Settings > Text Editing turns the counts on and off for functions, classes and structs, modules and representations, and member variables. Counts for member variables are off by default. (26A0134.093)
- Peek Definition in the Navigate menu (Option-Control-Command-J), Option-Command-click, or the context menu opens the definition in an editable block under the line. Edits change the file itself and are saved with Command-S. Several places show as a list, Open in Tab opens the file, Esc closes the block, and you can resize it. (26A0134.094)
- Code lens counts, the call and type hierarchy, and Find Call Hierarchy are now available when the clangd index is already up to date, instead of waiting for indexing. (26A0134.095)
- The source editor now draws all text with CoreText, including folds, carets, wrapped rows, and snippets. (26A0134.096)

##### Known Issues

- If you revert or reload a file in Source Control while it's shown in Peek Definition, the peek keeps the old text, and edits made there afterward aren't saved. (26A0134.097)

  **Workaround:** Close the peek with Esc and open it again after the revert.

- Peek Definition doesn't open for a call on the last line of a file. (26A0134.098)
- Rename is unavailable until clangd finishes indexing or while a build or deploy runs. Renaming a symbol that isn't a representation doesn't change `.cfg` files. (26A0122.169)
- Live markers appear only for files under `Src/` that you save in the editor. Files changed by git or a rename get none, and a save during a refresh build loses its markers when the new host takes over. (26A0134.099)
- Completion waits up to 20 seconds for the first analysis of a file by clangd. (26A0122.171)
- Option-click might highlight only the clicked name if it comes from a macro, such as `theX`. (26A0122.173)
- The page guide and tab stops might drift on lines with inlay hints. (26A0122.174)
- In SimRobot.app, the external app, the CABSL graph shows the code only and has no live view of the active state. (26A0122.404)

#### Tactics

##### New Features

- Tactics and set plays in `Config/Behavior` now open on a field, with a switch to Source. The field shows each position with its role and priority, the ball, and the start position. (26A0122.405)
- Dragging a position now snaps it to a field symbol from `fieldDimensions.cfg`, such as a penalty mark or a goal line, and writes the symbol, so the set play fits every field size. Hold Option to place a position freely. (26A0122.406)
- Show Tactic now shows the positions of the tactic behind a set play, and Mirror shows the set play mirrored. Reset to Tactic in the inspector removes the override of the selected position. (26A0122.407)
- The Priority Groups section of the inspector now shows the roles of each group, and you can drag the groups to reorder them. Needs sets the lowest priority a set play requires. (26A0122.408)
- Free kicks now show their Preconditions, checked while the game is stopped, and their Invariants, checked while it runs, as areas on the field. Angle conditions appear as rays from the goal. (26A0122.409)
- The inspector now adds and removes the conditions of a free kick and edits their values. (26A0122.410)
- Strategies now open in an overview of their tactics with the transitions between them, and cards for own and opponent set plays with their tactic and weight. (26A0122.411)
- The new Add to Strategy menu adds a set play to a list of the strategy, and the inspector edits its weight. Remove from Strategy is in the context menu of a card. (26A0122.412)
- Tactics, set plays, and strategies are now checked while you edit them, with the rules of the C++ code. Warnings appear in the Issues navigator. (26A0122.413)
- The check also warns when the start position of a set play isn't a position of its tactic, and when the preconditions of a free kick reach outside its invariants. (26A0122.414)

##### Known Issues

- You can only choose among the tactic and set play types of the C++ code. A new type needs a change to the C++ code. (26A0122.415)

#### Terminal

##### New Features

- The new Terminal tab runs your login shell in the repository root. (26A0122.181)
- The new toolbar button opens the tab and raises the bottom area. Leaving the tab restores the earlier height. (26A0122.183)

#### Testing

##### New Features

- The new Tests navigator lists the `TEST`, `TEST_F`, `TEST_P`, and `GTEST_TEST` macros under `Src/Apps/Tests`. (26A0122.186)
- Test (Command-U) now opens the navigator and starts a run. The navigator also has Play and Stop buttons. (26A0122.187)
- Tests now turn green or red from the output of gtest and XCTest, and an output pane shows the run. A failed run also shows its count of passed and failed tests. (26A0122.188)

##### Known Issues

- Test doesn't run `Make/macOS/generate` first. (26A0122.190)

#### Updates

##### New Features

- B-Editor now checks for updates every day and downloads them in the background. (26A0122.191)
- A new build now installs when you quit, or at once with Install and Relaunch. (26A0122.192)
- The new update window shows the release notes and contains Skip This Version, Remind Me Later, and Install Update. If the update is already downloaded, closing the window installs it on quit. (26A0122.193)
- A background update now waits for a running build, deploy, debug session, or SimRobot before it relaunches. The update window shows what it's waiting for. (26A0122.194)
- A relaunch now asks first when a command is running in the Terminal tab. (26A0122.195)
- If the app doesn't quit for an update, the window now offers Try Again. (26A0122.196)
- You can now choose the Release, Release Candidate, Beta, or Alpha channel in the Updates tab. Each channel also receives the more stable builds. (26A0122.197)
- The new Updates tab shows the installed build and the last check, turns automatic checks and downloads on or off, and contains Check Now. (26A0122.198)
- The toolbar and the Check for Updates menu item now show when an update is available. (26A0122.199)
- B-Editor now installs an update only when its EdDSA signature is valid. (26A0122.417)

#### Workspace

##### New Features

- The new navigator contains multiple tabs: (26A0122.200)
  - Project (Command-1)
  - Source Control (Command-2)
  - Bookmarks (Command-3)
  - Find (Command-4)
  - Issues (Command-5)
  - Tests (Command-6)
  - Debug (Command-7)
  - Breakpoints (Command-8)
  - Reports (Command-9)
- Filter in Navigator (Option-Command-J) and Reveal in Project Navigator (Shift-Command-J) are now available. (26A0122.201)
- The new inspector shows Document (Option-Command-1) and History (Option-Command-2). (26A0122.202)
- The Document inspector now shows the name, type, group, path, counterpart, and last commit of a file. (26A0122.418)
- You can show or hide the navigator (Command-0), the inspector (Option-Command-0), and the bottom area (Shift-Command-Y). (26A0122.203)
- A sidebar button at the top left now hides and shows the navigator, like Command-0. While the navigator is hidden, Run and Stop are in the toolbar. (26A0134.100)
- The new bottom area contains the Build, SimRobot, Deploy, and Terminal tabs, and an lldb tab while SimRobot is paused. (26A0122.204)
- The bottom area now has a filter and Clear Console (Command-K). Its height persists between launches. (26A0122.205)
- The debug bar also shows the step buttons while paused, the position of the caret, and the current branch. (26A0122.206)
- Open files now appear as tabs with a dot for unsaved changes. Previous Tab (Shift-Command-Left Bracket) and Next Tab (Shift-Command-Right Bracket) switch between them. (26A0122.207)
- You can now open an empty tab with New Tab (Command-T) or the add button in the tab bar. A middle click closes a tab. (26A0122.419)
- The new Add Editor on Right (Control-Command-T) in the View menu and the toolbar splits the editor into up to 3 panes. Each pane has its own tabs, and a pane closes with its last tab. (26A0122.420)
- The new jump bar above the editor shows the path of the file. (26A0122.208)
- Each item of the jump bar now opens a menu. A folder lists its contents, the file lists the files next to it, and the last item lists the functions of the file. (26A0122.421)
- The related items button at the start of the jump bar now lists counterparts, recent files, and the files the open file includes. (26A0122.422)
- Back (Control-Command-Left) and Forward (Control-Command-Right) now move through your history of files and the project editor. (26A0122.209)
- The toolbar now shows the status of builds, runs, deploys, and indexing. (26A0122.210)
- The toolbar now shows the number of errors and warnings. Click a count to open the Issues navigator. (26A0122.423)
- The Issues navigator now always opens on Live and lists the errors and warnings of every file: open files, closed files with the time of their last check, and files you never opened. (26A0134.101)
- The picker in the Issues navigator is now a filter: Live, All, and Build. After a failed build, the navigator stays on Live and shows the number of build errors with Show. (26A0134.102)
- Shell scripts, `threads.cfg`, tactics, `.con` scripts, and `.cfg` files are now checked in the background when you open the repository and when they change. A `.cfg` parse error is an error, and an unknown key is a warning. The checks pause while a build runs and on battery in Low Power Mode. (26A0134.103)
- The error and warning counts in the toolbar now cover all files, and hovering them lists where the issues come from. Next Issue and Previous Issue walk all files. (26A0134.104)
- After you save a header under `Src`, the editor asks clangd to check up to 20 `.cpp` files that include it, nearest includes first, in the background. Their issues appear in the Issues list with the note "checked after saving" and the header's name. (26A0134.105)
- The new Check Project in the Product menu checks every C++ file of the compile database in the background, with progress, a time estimate, and Stop. Like the other background checks, it waits while a build runs and on battery in Low Power Mode. (26A0134.106)
- The Issues navigator now lists representations that no module uses and modules that no scenario runs. Ignored entries are kept in the editor's settings, not in the repository. (26A0134.107)
- The new Notes segment in the Issues navigator lists the TODO and FIXME comments of the repository by file. Notes never count in the toolbar badge. (26A0134.108)
- A finding that appears both in a module header and in `threads.cfg` now counts once in the toolbar. (26A0134.109)
- The Reports navigator now lists builds, deploys, runs, tests, Generate Project, and Git operations by day. Select a report to see its summary, duration, and full log. (26A0122.424)
- The editor column now keeps a width of 500 pt. When the window gets narrower, the inspector collapses first, then the navigator, and the canvas hides before both. They return when the window grows. (26A0122.425)
- The jump bar now collapses leading folders into one ellipsis when the path is too long. (26A0122.426)
