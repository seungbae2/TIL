# Flutter Widget Lifecycle

## StateLess Widget Lifecycle

Create → build() → dispose

## Stateful Widget Lifecycle

Create Widget → Create State<Widget> → initState() → build() [ → setState() / didUpdatedWidget() → build() ] → deactivate → dispose() → Dispose