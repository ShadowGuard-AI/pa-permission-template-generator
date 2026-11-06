# pa-permission-template-generator
Generates permission templates (e.g., JSON, YAML) based on existing permission assignments, facilitating consistent permission application across similar roles or resources. Uses a Jinja2 template to write the output. - Focused on Tools for analyzing and assessing file system permissions

## Install
`git clone https://github.com/ShadowGuard-AI/pa-permission-template-generator`
`cd pa-permission-template-generator`
`pip install -r requirements.txt`

## Usage
`python3 main.py --source-dir <dir> --output-file <file> --template-file <file.j2> [--exclude-patterns <pattern> ...] [--output-format json]`

The template is rendered with the collected permission records bound to the name `files`. The output format contract: the rendered template text must itself parse as valid data in the chosen output format (JSON for `--output-format json`, YAML for `--output-format yaml`). The rendered data is parsed and re-dumped to the output file; a render that is not valid data in the chosen format fails with exit 1 and writes nothing. YAML mode requires PyYAML, which is listed in requirements.txt. If no files are analyzed, the run exits 1, writes no output, and prints a no files analyzed line. The output file must not be the template file or a file inside the source directory; such a run refuses at exit 1.

Note: a full live run was not possible in this pass because jinja2 and pathspec are not installed in this environment and installs were out of scope, so the template render path is untested here. Syntax check and help output were verified.

## Parameters
- `-h`: Show help message and exit
- `--source-dir` (required): Path to the directory to analyze permissions from.
- `--output-file` (required): Path to the output file to write the permission template to.
- `--template-file` (required): Path to the Jinja2 template file to use for generating the template.
- `--exclude-patterns` (optional, default none): List of file patterns to exclude from permission analysis (e.g., '*.log', 'temp/*').
- `--output-format` (optional, default `json`): Format of the output file (json or yaml). Requires PyYAML to be installed for yaml.

## License
Licensed under the MIT License, see LICENSE.
