# readme2tex
Renders LaTeX for Github Readmes

<p align="center"><img src="https://rawgit.com/in	git@github.com:vijayshankarv/notes/svgs/svgs/d27ecd9d6334c7a020001926c8000801.svg?invert_in_darkmode" align=middle width=159.69013499999997pt height=30.925784999999998pt/></p>

<p align="center"><img src="https://rawgit.com/in	git@github.com:vijayshankarv/notes/svgs/svgs/a00f34be6b1ce8e4820c9852c5e6163e.svg" align=middle width=748.4961pt height=75.554985pt/></p>

<sub>**Make sure that pdflatex is installed on your system.**</sub>

----------------------------------------

`readme2tex` is a Python script that "texifies" your readme. It takes in Github Markdown and
replaces anything enclosed between dollar signs with rendered <img src="https://rawgit.com/in	git@github.com:vijayshankarv/notes/svgs/svgs/c068b57af6b6fa949824f73dcb828783.svg?invert_in_darkmode" align=middle width=42.058170000000004pt height=22.40699999999997pt/>.

In addition, while other Github TeX renderers tend to give a jumpy look to the compiled text, 
<p align="center">
<img src="http://i.imgur.com/XSV1rPw.png?1" width=500/>
</p>

`readme2tex` ensures that inline mathematical expressions
are properly aligned with the rest of the text to give a more natural look to the document. For example,
this formula <img src="https://rawgit.com/in	git@github.com:vijayshankarv/notes/svgs/svgs/24a7d013bfb0af0838f476055fc6e1ef.svg?invert_in_darkmode" align=middle width=14.297414999999997pt height=30.588690000000003pt/> is preprocessed so that it lines up at the correct baseline for the text.
This is the one salient feature of this package compared to the others out there.

### Installation

Make sure that you have Python 2.7 or above and `pip` installed. In addition, you'll need to have the programs `latex` 
and `dvisvgm` on your `PATH`. In addition, you'll need to pre-install the `geometry` package in <img src="https://rawgit.com/in	git@github.com:vijayshankarv/notes/svgs/svgs/c068b57af6b6fa949824f73dcb828783.svg?invert_in_darkmode" align=middle width=42.058170000000004pt height=22.40699999999997pt/>.

To install `readme2tex`, you'll need to run

```bash
sudo pip install readme2tex
```

or, if you want to try out the bleeding edge,

```bash
git clone https://github.com/leegao/readme2tex
cd readme2tex
python setup.py develop
```

To compile `INPUT.md` and render all of its formulas, run

```bash
python -m readme2tex --output README.md INPUT.md
```

If you want to do this automatically for every commit of INPUT.md, you can use the `--add-git-hook` command once to
set up the post-commit hook, like so

```bash
git stash --include-untracked
git branch svgs # if this isn't already there

python -m readme2tex --output README.md --branch svgs --usepackage tikz INPUT.md --add-git-hook

# modify INPUT.md

git add INPUT.md
git commit -a -m "updated readme"

git stash pop
```

and every `git commit` that touches `INPUT.md` from now on will allow you to automatically run `readme2tex` on it, saving
you from having to remember how `readme2tex` works. The caveat is that if you use a GUI to interact with git, things
might get a bit wonky. In particular, `readme2tex` will just assume that you're fine with all of the changes and won't
prompt you for verification like it does on the terminal.

<p align="center">
<a href="https://asciinema.org/a/2am62r2x2udg1zqyb6r3kpm1i"><img src="https://asciinema.org/a/2am62r2x2udg1zqyb6r3kpm1i.png" width=600/></a>
</p>

You can uninstall the hook by deleting `.git/hooks/post-commit`. See `python -m readme2tex --help` for a list
of what you can do in `readme2tex`.

### Examples:

Here's a display level formula
<p align="center"><img src="https://rawgit.com/in	git@github.com:vijayshankarv/notes/svgs/svgs/32737e0a8d5a4cf32ba3ab1b74902ab7.svg?invert_in_darkmode" align=middle width=127.89182999999998pt height=39.30498pt/></p>

The code that was used to render this formula is just

    $$
    \frac{n!}{k!(n-k)!} = {n \choose k}
    $$

<sub>*Note: you can escape \$ so that they don't render.*</sub>

Here's an inline formula. 

> It is well known that if <img src="https://rawgit.com/in	git@github.com:vijayshankarv/notes/svgs/svgs/162f63774d8a882cc15ae1301cfd8ac0.svg?invert_in_darkmode" align=middle width=119.01186pt height=26.70657pt/>, then <img src="https://rawgit.com/in	git@github.com:vijayshankarv/notes/svgs/svgs/584fa2612b78129d140fb208e9d76ae9.svg?invert_in_darkmode" align=middle width=112.3584pt height=33.20525999999999pt/>.

The code that was used to render this is:

    It is well known that if $ax^2 + bx + c = 0$, then $x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$.

Notice that the formulas line up with the baseline of the text, even when the height of these two images are different.

Sometimes, you might run into formulas that are bottom-heavy, like <img src="https://rawgit.com/in	git@github.com:vijayshankarv/notes/svgs/svgs/4cb4ead947a07837121937c807973436.svg?invert_in_darkmode" align=middle width=47.639295000000004pt height=37.03193999999999pt/>. Here, `readme2tex`
can compute the correct offset to align this formula to the baseline of your paragraph of text as well.

#### Tikz (Courtesy of http://www.texample.net/)

Did you notice the picture at the top of this page? That was also generated by <img src="https://rawgit.com/in	git@github.com:vijayshankarv/notes/svgs/svgs/c068b57af6b6fa949824f73dcb828783.svg?invert_in_darkmode" align=middle width=42.058170000000004pt height=22.40699999999997pt/>. `readme2tex` is capable of
handling Tikz code. For reference, the picture

<p align="center"><img src="https://rawgit.com/in	git@github.com:vijayshankarv/notes/svgs/svgs/522cbfbc866df378cb95b2ef083131b2.svg" align=middle width=741.26415pt height=75.554985pt/></p>

is given by the tikz code

    \begin{tikzpicture}
    \newcounter{density}
    \setcounter{density}{20}
        \def\couleur{red}
        \path[coordinate] (0,0)  coordinate(A)
                    ++( 60:6cm) coordinate(B)
                    ++(-60:6cm) coordinate(C);
        \draw[fill=\couleur!\thedensity] (A) -- (B) -- (C) -- cycle;
        \foreach \x in {1,...,15}{%
            \pgfmathsetcounter{density}{\thedensity+10}
            \setcounter{density}{\thedensity}
            \path[coordinate] coordinate(X) at (A){};
            \path[coordinate] (A) -- (B) coordinate[pos=.15](A)
                                -- (C) coordinate[pos=.15](B)
                                -- (X) coordinate[pos=.15](C);
            \draw[fill=\couleur!\thedensity] (A)--(B)--(C)--cycle;
        }
    \end{tikzpicture}

We can see a few other examples, such as this graphical proof of the Pythagorean Theorem.

<p align="center"><img src="https://rawgit.com/in	git@github.com:vijayshankarv/notes/svgs/svgs/e148d2d3bb31215788cc03f9b472e5ba.svg?invert_in_darkmode" align=middle width=698.60835pt height=213.63705pt/></p>

How about a few snowflakes?

<p align="center"><img src="https://rawgit.com/in	git@github.com:vijayshankarv/notes/svgs/svgs/eb57748cb91d08bfc997b0d70f7f2774.svg?invert_in_darkmode" align=middle width=688.8321pt height=469.16595pt/></p>

### Usage

    python -m readme2tex --output README.md [READOTHER.md]

It will then look for a file called `readother.md` and compile it down to a readable Github-ready
document.

In addition, you can specify other arguments to `render.py`, such as:

* `--readme READOTHER.md` The raw readme to process. Defaults to `READOTHER.md`.
* `--output README.md` The processed readme.md file. Defaults to `README_GH.md`.
* `--usepackage tikz` Addition packages to use during <img src="https://rawgit.com/in	git@github.com:vijayshankarv/notes/svgs/svgs/c068b57af6b6fa949824f73dcb828783.svg?invert_in_darkmode" align=middle width=42.058170000000004pt height=22.40699999999997pt/> compilation. You can specify this multiple times.
* `--svgdir svgs/` The directory to store the output svgs. The default is `svgs/`
* `--branch master` *Experimental* Which branch to store the svgs into, the default is just master.
* `--username username` Your github username. This is optional, and `render.py` will try to infer this for you.
* `--project project` The current github project. This is also optional.
* `--nocdn` Ticking this will use relative paths for the output images. Defaults to False.
* `--htmlize` Ticking this will output a `md.html` file so you can preview what the output looks like. Defaults to False.
* `--valign` Ticking this will use the `valign` trick (detailed below) instead. See the caveats section for tradeoffs.
* `--rerender` Ticking this will force a recompilation of all <img src="https://rawgit.com/in	git@github.com:vijayshankarv/notes/svgs/svgs/c068b57af6b6fa949824f73dcb828783.svg?invert_in_darkmode" align=middle width=42.058170000000004pt height=22.40699999999997pt/> formulas even if they are already cached.
* `--bustcache` Ticking this will ensure that Github renews its image cache. Github may sometimes take up to an hour for changed images to reappear. This is usually not necessary unless you've made stylistic changes.
* `--add-git-hook` Ticking this will generate a post-commit hook for git that runs readme2tex with the rest of the specified arguments after each `git commit`.
* `--pngtrick` Ticking this will generate `png` files instead of `svgs` for the formulas.

My usual workflow is to create a secondary branch just for the compiled svgs. You can accomplish this via

    python -m readme2tex --branch svgs --output README.md

However, be careful with this command, since it will switch over to the `svgs` branch without any input from you.

#### Relative Paths

If you're on a private repository or you want to, for whatever reason, use relative paths to resolve your images, you can
do so by using the combination

    python -m readme2tex --branch master --nocdn --pngtrick ...

which will output `pngs` relative to your `README.md`.

Due to security considerations, Github will not resolve `svgs` relatively, which means that private repositories will
be locked out of the usual `svg` workflow. Using the `--branch master --nocdn --pngtrick` combination will get around
this restriction.

### Troubleshooting

#### Tikz

If your Tikz drawings don't show up, there's a good chance that you either don't have Ghostscript installed or
`dvisvgm` isn't picking it up for whatever reason. This is most likely to happen on some installations of TexLive
on OSX.

Check to see if `ps` is included in the list when you run

```bash
# dvisvgm -l
bgcolor    background color special
color      complete support of color specials
dvisvgm    special set for embedding raw SVG snippets
em         line drawing statements of the emTeX special set
html       hyperref specials
pdf        pdfTeX font map specials
ps         dvips PostScript specials <<<
tpic       TPIC specials
```

If not, try installing it (either `apt-get`, `yum`, or `brew`). Furthermore, if you are on OSX, make sure to add the
following to your `~/.bash_profile`

```bash
export LIBGS=/usr/local/lib/libgs.dylib
```

where `/usr/local/lib/libgs.dylib` is the location where `libgs.dylib` is installed.

#### I'm seeing weird formatting from time to time.

Make sure that if you have a `<p>...</p>` tag somewhere, you leave at least one blank line after the closing tag.

#### I ran `--add-git-hook`, but the post-commit hook isn't running after committing.

```bash
chmod +x .git/hooks/post-commit
```

#### I ran `readme2tex` and got a traceback somewhere.

Unfortunately, this script still has a few kinks and bugs that I need to iron out. In the mean time, if the `pypi` releases
aren't working for you, you should switch over to the development version to see if the bugs have been squashed:

```bash
git clone https://github.com/leegao/readme2tex
cd readme2tex
python setup.py develop
```

### Technical Tricks

#### How can you tell where the baseline of an image is?

By prepending every inline formula with an anchor. During post-processing, we can isolate the anchor, which
is fixed at the baseline, and crop it out. It's super clowny, but it does the job.

#### Caveats

Github does not allow you to pass in custom style attributes to your images. While this is useful for security purposes,
it makes it incredibly difficult to ensure that images will align correctly to the text. `readme2tex` circumvents this
using one of two tricks:

1. In Chrome, the attribute `valign=offset` works for `img` tags as well. This allows us to shift the image directly.
Unfortunately, this is not supported within any of the other major browsers, therefore this mode is not enabled by
default.
2. In every (reasonably modern) browser, the `align=middle` attribute will vertically center an image. However, the
definition of the vertical "center" is different. In particular, for Chrome, Firefox, (and probably Safari), that center
is the exact middle of the image. For IE and Edge however, the center is about 5 pixels (the height of a lower-case character)
above the exact center. Since this looks great for non-IE browsers, and reasonably good on Edge, this is the default
rendering method. The trick here is to pad either the top or the bottom of the image with extra spaces until the
baseline of the formula is at the center. For most formulas, this works great. However, if you have a tall formula,
like <img src="https://rawgit.com/in	git@github.com:vijayshankarv/notes/svgs/svgs/bdd0f9b91b7fff7fe5a2b1b7684a96ef.svg?invert_in_darkmode" align=middle width=56.16665999999999pt height=71.68952999999999pt/>, you'll notice that there might be a lot
of slack vertical spacing between these lines. If this is a deal-breaker for you, you can always try the `--valign True`
mode. For most inline formulas, this is usually a non-issue.

#### How to compile this document
Make sure that you have the `tikz` and the `xcolor` packages installed locally.

    python -m readme2tex --usepackage "tikz" --usepackage "xcolor" --output README.md --branch svgs

and of course

    python -m readme2tex --usepackage "tikz" --usepackage "xcolor" --output README.md --branch svgs --add-git-hook

For the `png` relative mode, use

    python -m readme2tex --usepackage "tikz" --usepackage "xcolor" --output README.md --branch master --nocdn --pngtrick

----------------------------------------

<p align="center"><img src="https://rawgit.com/in	git@github.com:vijayshankarv/notes/svgs/svgs/48ab6ba0b4263d6ecddedfd213f66ff5.svg?invert_in_darkmode" align=middle width=1129.0752pt height=292.5417pt/></p>