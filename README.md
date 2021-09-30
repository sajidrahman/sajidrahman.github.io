### This repository contains source codes for my site hosted here: https://www.cise.ufl.edu/~msr/



### Notes:

- Currently I'm using rsync to deploy the `public` folder to remote server.
- I've taken a lot of tips from this [great post](https://matteocourthoud.github.io/post/website/). 🙏 
- Faced this issue after cloning the [original repo](https://github.com/wowchemy/starter-hugo-academic) from wowchemy, solved the issue by following this [guideline](https://wowchemy.com/docs/guide/troubleshooting/#error-go-executable-not-found).
- Created the deployment script (`deploy` file) by following this [guide](https://gohugo.io/hosting-and-deployment/deployment-with-rsync/).
- Updated the publication section by this [guideline](https://www.emmanuelteitelbaum.com/post/managing-pubs-academic-website/).
- To build, run `hugo`
- To publish, run `./deploy`

### Troubleshooting

1. `Error: from config: failed to resolve output format "headers" from site config`

   Solution:

   - Temporarily remove the “WebAppManifest”, “redirects”, “headers” output types from your config.yaml and run:

   ```markdown
   
   hugo mod clean
   hugo mod tidy
   ```

   - Check that hugo now runs OK with `hugo server` or blogdown and then add the output types back into your config.yaml.

[Reference](http://www.mysmu.edu/faculty/jwwang/post/building-your-website-with-hugo-and-rmarkdown/)

