# pptx deck builder

Builds a 56 slide thesis defence presentation from a written spec, in Python, with no PowerPoint involved until the file opens.

## Why generate a deck instead of making one

I had a deck to build for a defence on data driven fuzzy control of a three tank rig, and I had gone through the usual cycle: the supervisor asks for one change to the structure, and you spend an evening dragging boxes on 56 slides to match. Doing it by hand does not scale to revision three.

So the deck became a build artifact. `SPEC.md` describes what the presentation says. `build_deck.py` turns that into a `.pptx`. When the content changes I edit the spec and rebuild, and every slide picks up the change consistently because the layout lives in code rather than in my memory of what I did on slide 31.

## What it handles

Embedded fonts, so the deck renders the same on the examiner's machine as on mine. Morph transitions between related slides, which python-pptx does not expose directly and which had to be written into the XML by hand. Rendered equations, because a control theory defence is mostly equations and screenshotting them from LaTeX looks exactly as bad as it sounds. Full bleed imagery with text placed over it rather than beside it.

## Layout

    build_deck.py     the main builder, slide by slide
    decklib.py        layout primitives: text blocks, image fills, transitions, equations
    build_3d.py       generates the 3D renders used as slide backgrounds
    extract_figs.py   pulls figures out of the thesis PDF so they stay in sync
    SPEC.md           the content spec the deck is built from

## Running it

    pip install python-pptx pillow
    python build_deck.py

The image assets and the generated `.pptx` are not in this repository, since they are specific to one thesis and run to a couple of hundred megabytes. The code is the reusable part.

## Honest limitation

This is not a general purpose deck framework. It was written for one presentation and the layout choices are baked to that content. What generalises is `decklib.py` and the approach: describe the deck, build it, never drag a box again.
