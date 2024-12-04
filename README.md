# Psych-DS Documentation

This repository contains the source files for the [Psych-DS documentation website](https://psychds-docs.readthedocs.io/). The documentation is built using MkDocs and hosted on ReadTheDocs.

## Local Development Setup

1. Clone the repository:
```bash
git clone https://github.com/psych-ds/psychds-docs.git
cd psychds-docs
```

2. Create and activate a virtual environment (recommended):
```bash
python -m venv venv
# On Windows
.\venv\Scripts\activate
# On Unix or MacOS
source venv/bin/activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Start the local development server:
```bash
mkdocs serve
```

 The site will now be running at `http://127.0.0.1:8000` and will automatically rebuild when you save changes to any source files.


## Contributing

1. **Fork and Clone**: Fork this repository and clone it locally.

2. **Create a Branch**: Create a branch for your changes:
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make Changes**: 
   - Documentation is written in Markdown
   - Add new pages in the appropriate directory
   - Update `.pages.yml` if you add new files
   - Images  go in `docs/images/`

4. **Test Locally**: Always test your changes using `mkdocs serve`

5. **Submit a Pull Request**: Push your changes and create a pull request

## Build Configuration

The `mkdocs.yml` file controls the site configuration. Key settings include:

- Theme configuration
- Plugins
- Site metadata

## Deployment

The documentation is automatically built and deployed to ReadTheDocs when changes are pushed to the main branch. No manual deployment is necessary.

## Writing Guidelines

- Use clear, concise languag
- Follow the existing document structure

## Need Help?

- Open an issue in this repository
- Check the [MkDocs documentation](https://www.mkdocs.org/)
- Review the [ReadTheDocs guide](https://docs.readthedocs.io/)
