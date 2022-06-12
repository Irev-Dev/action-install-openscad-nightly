### Install OpenSCAD nightly

Action that installs OpenSCAD nighly, and other things (like xvfb) needed to use OpenSCAD in github workflows

Example would be to produce stl artifacts from a `.scad` script i.e.
```yml
name: Create STL and publish release
on:
  push:
    tags:
    - '*'
jobs:
  create-n-publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: Irev-Dev/action-install-openscad-nightly@v0.0.1
      - name: create stl
        run: xvfb-run --auto-servernum --server-args "-screen 0 1024x768x24" openscad-nightly -o ./output.stl -P default ./demo.scad
      - uses: ncipollo/release-action@v1
        with:
          artifacts: output.stl
          token: ${{ secrets.GITHUB_TOKEN }}
```

note `xvfb-run` is necessary.
