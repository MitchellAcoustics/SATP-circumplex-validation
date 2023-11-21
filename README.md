# SATP circumplex validation

 Code for the validation of tranlastions of the Soundscape Circumplex

## Setup

This repository is built using [Quarto](https://quarto.org/), [R](https://www.r-project.org/), and [Python](https://www.python.org/). Package installation was managed using `renv`, both for the R and Python environments (see this help page from Quarto for more information: <https://quarto.org/docs/projects/virtual-environments.html#using-renv>).

You should be able to set up the whole project environment using `renv::restore()`. [See the documentation page for more detailed instructions](https://rstudio.github.io/renv/reference/restore.html).

```r
> renv::restore()
```

### Manual setup

Below we document the commands that were used to set up the project. Note that the `renv` lockfiles are included in the repository, so you should be able to skip the installation steps and just run the code.

```bash
$ R # Start a new R session
```

```r
> install.packages("renv") # If you need to install renv, skip if you already have it

> renv::init() # Initialize renv
```

This will create an `.Rprofile` file in the directory root. This file is used to automatically activate the `renv` environment when you open the project (with `source("renv/activate.R")`). You can also run `renv::activate()` to activate the environment manually.

We will require the following R packages:

```r
> renv::install(c("tidyverse", "readxl", "here", "knitr", "devtools"))
> renv::install("MitchellAcoustics/CircE-R") # CircE is no longer available 
# on CRAN, so we install from the mirror on my GitHub
```

Next, set up the Python environment. This will likely prompt you to select a Python version to use. I recommend using 3.11, managed with `pyenv`.

```r
> renv::use_python(name=".venv")
```

At the core, all this does is create a Python virtualenv at `.venv`, just like setting up a Python environment normally. But by linking it with `renv` we can do some extra management of both the R and Python environments together. Feel free to manage your Python environment some other way if you prefer.

Activate the Python environment:

```bash
$ source .venv/bin/activate
$ python --version # Check that the correct Python version is being used
Python 3.11.4
```

We will require the following Python packages:

```bash
$ pip install 'pandas[excel]' seaborn scipy numpy circumplex matplotlib jupyter
Successfully installed circumplex-0.1.3 contourpy-1.2.0 cycler-0.12.1 defusedxml-0.7.1 et-xmlfile-1.1.0 fonttools-4.45.0 kiwisolver-1.4.5 matplotlib-3.8.2 numpy-1.26.2 odfpy-1.4.1 openpyxl-3.1.2 packaging-23.2 pandas-2.1.3 pillow-10.1.0 pyparsing-3.1.1 python-dateutil-2.8.2 pytz-2023.3.post1 pyxlsb-1.0.10 scipy-1.11.4 seaborn-0.13.0 six-1.16.0 tzdata-2023.3 xlrd-2.0.1 xlsxwriter-3.1.9
```

Then write these out to a `requirements.txt` file using `renv::snapshot()`:

```r
> renv::snapshot()
Wrote Python packages to "~/Documents/GitHub/SATP-circumplex-validation/requirements.txt".
```

or using `pip freeze`:

```bash
$ pip freeze > requirements.txt
```

### Quarto setup

Finally, we need to install Quarto. This is a bit more involved, so I recommend following the [Quarto installation instructions](https://quarto.org/docs/getting-started/installation.html) for your platform.

Once you have Quarto installed and this repository setup, you can run the following to add the Elsevier journal templated we used to render the PDF:

```bash
$ quarto add quarto-journals/elsevier
[✓] Extension installation complete.
Learn more about this extension at https://www.github.com/quarto-journals/elsevier
```
