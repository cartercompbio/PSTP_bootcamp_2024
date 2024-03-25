# Jupyter Notebook Tutorial

Jupyter Notebooks offer a flexible and interactive environment for data analysis and visualization in Python, R and other languages. This tutorial will guide you through the basics of Jupyter Notebook, an essential tool in data science and scientific computing.

### Launching Jupyter

Similar to what we did in the HPC tutorial, let's launch Jupyter for Python using our python_3_8 conda environment. Set the walltime to 1 hour 30 min.

'galyleo launch --account htl179 --qos hotel --cpus 1 --memory 8 --time-limit 01:30:00 --partition hotel --conda-env python_3_8 --env-modules slurm/tscc/23.02.7 --conda-init /tscc/nfs/home/etrain104/anaconda/etc/profile.d/conda.sh'

### Exploring the Interface

- When you first open a Jupyter Notebook, you'll see a user-friendly interface where you can write and execute code and text.
- Make a folder called `jupyter_tutorial` and start a new Python notebook inside of it.
- Jupyter will open in whatever directory you are located in when it is launched. 

### Understanding Cells and Kernels

- **Cells:** The building blocks of a notebook, cells can contain either executable code or formatted text.
- **Kernels:** A kernel is a computational engine that executes the code in your notebook. Each notebook runs on a kernel specific to the programming language you're using.

#### Working with Cells

- **Code Cells:** These cells contain code that you can execute. The output is displayed right below the cell.
- **Markdown Cells:** These cells contain text formatted using Markdown. When executed, they display the formatted text inline.

#### Trying Out a Code Cell

- Type `print('Hello World!')` into a code cell and execute it (using the run button or `Ctrl + Enter`). You should see the output displayed below the cell.

Challenge: Figure out how to run a Markdown cell. 

### Keyboard Shortcuts

- Jupyter offers numerous keyboard shortcuts that can speed up your workflow:
  - `Esc`/`Enter`: Toggle between edit mode (green outline) and command mode (blue outline).
  - `A`/`B`: Insert a new cell above/below the active cell.
  - `M`: Change the cell to Markdown.
  - `Y`: Change the cell to code.
  - `D + D`: Delete the active cell. (d twice)
  - `Z`: Undo cell deletion.

## Markdown Basics

- Markdown allows you to create formatted text using a simple and readable syntax.
- **Headers:** Use `#` for headers. More `#`s mean smaller headers.
- **Bold/Italic:** Use `**bold**` or `*italic*` to format text.
- **Lists:** Use `-` or `1.` to create bulleted or numbered lists.
- **Links:** Use `[text](URL)` to create hyperlinks.
- **Code:** Use backticks (`) to format code within text.

Challenge: Make the above paragraph in jupyter.

## Kernels

- The kernel executes your code and returns output. It retains state, so variables and functions defined in one cell can be used in others.

### Changing Kernels

- Jupyter supports kernels for different languages. You can change the kernel to fit your project's needs.

## Example Analysis

Let's perform a simple data analysis within a Jupyter Notebook:

1. **Setting Up:** Start with importing necessary libraries and loading your data.

    ```python
    import pandas as pd
    df = pd.read_csv('your_data.csv')
    ```

2. **Data Exploration:** Use commands like `df.head()` to examine the first few rows of your dataset.

3. **Data Visualization:** Leverage libraries like Matplotlib or Seaborn to create visualizations.

    ```python
    import matplotlib.pyplot as plt
    df.plot(kind='line')
    plt.show()
    ```

## Sharing Notebooks

- Jupyter Notebooks can be shared as `.ipynb` files or exported to formats like HTML or PDF.
- GitHub renders Jupyter Notebooks natively, making it an excellent platform for sharing your work.

## Conclusion

Jupyter Notebooks are a powerful tool for data analysis and scientific computing, offering a blend of code, text, and graphics in a single document.

