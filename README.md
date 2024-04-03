# Hello Rust in Python


This project exposes Rust apis to be used in Python.

The project was implement from watching youtube video at: [https://www.youtube.com/watch?v=lhfroHM6kEo](https://www.youtube.com/watch?v=lhfroHM6kEo)

## Get Started
1. Create a virtual environment to install `maturin`
```sh
# Create new virtual environment and activate it.
python3 -m venv venv
source venv/bin/activate
```

2. Install maturin now and create new project.
```sh
pip install maturin
maturin new hello_rust_in_python
cd hello_rust_in_python
```

3. You can edit or change your files as needed here. This is a simple rust project with `src/lib.rs` file:
```rust
use pyo3::prelude::*;

/// Formats the sum of two numbers as string.
#[pyfunction]
fn sum_as_string(a: usize, b: usize) -> PyResult<String> {
    Ok((a + b).to_string())
}

/// A Python module implemented in Rust.
#[pymodule]
fn hello_rust_in_python(_py: Python, m: &PyModule) -> PyResult<()> {
    m.add_function(wrap_pyfunction!(sum_as_string, m)?)?;
    Ok(())
}
```

4. Build a Python wheel from rust project
```sh
maturin build
pip install target/wheels/hello_rust_in_python-0.1.0-cp310-cp310-manylinux_2_34_x86_64.whl
```

5. Use our rust library in python now after opening python shell using `python3`:
Here is the python code to use our rust function.

```python
from hello_rust_in_python import sum_as_string

print(f"Result: {sum_as_string(3, 4)}")
```

