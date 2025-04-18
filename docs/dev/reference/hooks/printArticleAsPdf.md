---
title: "printArticleAsPdf"
description: "printArticleAsPdf hook"
tags: ["hook-module", "hook-article"]
aliases:
    - /reference/hooks/printArticleAsPdf/
    - /reference/hooks/printarticleaspdf/
---


The `printArticleAsPdf` hook is triggered when an article should be exported as
PDF. It passes the article text and the article object as arguments and does not
expect a return value. Use it to override the internal PDF functionality.

{{% notice note %}}
Using the `printArticleAsPdf` hook has been deprecated and will no longer work in Contao 5.0.
{{% /notice %}}


## Parameters

1. *string* `$articleContent`

    The compiled article content.

2. *\Contao\ModuleArticle* `$module`

    Instance of the `\Contao\ModuleArticle` module responsible for producing the 
    front end output of an article.


## Example

```php
// src/EventListener/PrintArticleAsPdfListener.php
namespace App\EventListener;

use Contao\CoreBundle\DependencyInjection\Attribute\AsHook;
use Contao\ModuleArticle;

#[AsHook('printArticleAsPdf')]
class PrintArticleAsPdfListener
{
    public function __invoke(string $articleContent, ModuleArticle $module): void
    {
        // Trigger your own PDF engine and exit
        exit;
    }
}
```

* [\Contao\TcpdfBundle\EventListener\PrintArticleAsPdfListener#L31-L125](https://github.com/contao/tcpdf-bundle/blob/1.1/src/EventListener/PrintArticleAsPdfListener.php#L31-L125)


## References

* [\Contao\ModuleArticle#L296-L304](https://github.com/contao/contao/blob/4.7.6/core-bundle/src/Resources/contao/modules/ModuleArticle.php#L296-L304)
