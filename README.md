# gha-deploy-wagtail-zappa
A custom GitHub Action will deploy a Wagtail project to AWS Lambda

## Usage
The major tag version does not need to be changed.
The custom action will take the following inputs:
- `project-name `: name of the project
- `deployment-target `: either `staging` or `production`
- `aws-access-key-id `: Should be given using secrects
- `aws-secret-access-key `: Should be given using secrects
- `django-secret-key `: Should be given using secrects
- `uses-tailwind `: Optional. should be `false` (case sensitive) if the project does not use tailwind. Anything else will be interpreted as true.
- `elm-paths `: Optional. All paths to elm files ( /wagtail/{{ project-name }}/{{ folder }}/elm ) in project seperated by whitespace
- `elm-version `: Optional. Version number of elm.

## Example Usage

        ...

        steps:
        - name: Checkout
            uses: actions/checkout@v3
        
        - name: Custom Deploy Action
            uses: Funbit-AS/gha-deploy-wagtail-zappa@v1
            with:
                project-name: funbitno
                deployment-target: staging
                aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
                aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
                django-secret-key: ${{ secrets.DJANGO_SECRET_KEY }}
                uses-tailwind: True
                elm-paths: /wagtail/funbitno/projects/elm

## Release New Version
- Simply create a new version in the Github repository.
- The major tag (`v1`) will update automatically once the a new release has been created