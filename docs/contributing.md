---
id: contributing
title: Contribution Guidelines
---

import ReactGA from 'react-ga';

export const Logger = ({children}) => (
<>
<span>{ReactGA.initialize('UA-152867655-1')}</span>
<span>{ReactGA.pageview('Contributing')}</span>
</>
);

<Logger> Hi, I am logger</Logger>

# How to Contribute

You can always reach out to ankit@signoz.io to understand more about the repo and product. We are very responsive over email and [slack](https://signoz-community.slack.com/join/shared_invite/zt-kj26gm1u-Xe3CYxCu0bGXCrCqKipjOA#/).

- You can create a PR (Pull Request)
- If you find any bugs, please create an issue
- If you find anything missing in documentation, you can create an issue with label **documentation**

#### If you want to build any new feature, please create an issue with tag `enhancement`