---
title: "getImage"
description: "getImage hook"
tags: ["hook-image"]
aliases:
    - /reference/hooks/getImage/
    - /reference/hooks/getimage/
---


The `getImage` hook is triggered when a thumbnail is generated and allows you to
add a custom routine. It passes the path, the width and height, the mode, the
cache name and the file object as arguments and expects a path as return value.


{{% notice note %}}
Using the `executeResize` and `getImage` hooks has been deprecated and will no 
longer work in Contao 5.0. Use the `contao.image.resizer` service instead.
{{% /notice %}}


## Parameters

1. *string* `$originalPath`

    The image location, relative to Contao root.

2. *int* `$width`

    The target image width.

3. *int* `$height`

    The target image height.
    
4. *string* `mode`

    The resize mode.

5. *string* `$cacheName`

    The cache file name generated from source file name, width, height and mode
    setting.

6. *\Contao\File* `$file`

    A `\Contao\File` object from the source image.

7. *string* `$targetPath`

    The target location where the image should be stored. This will be `null` in
    most cases, if not you should ignore `$cacheName`.

8. *\Contao\Image* `$imageObject`
 
    The instance of the `\Contao\Image` class that triggered the hook.


## Return Values

If you want to override Contao's `Image::get` method, return a string to the new image. 
Otherwise return the boolean `false`.


## Example

```php
// src/EventListener/GetImageListener.php
namespace App\EventListener;

use Contao\CoreBundle\DependencyInjection\Attribute\AsHook;
use Contao\Image;
use Contao\File;

#[AsHook('getImage')]
class GetImageListener
{
    public function __invoke(
        string $originalPath, 
        int $width, 
        int $height, 
        string $mode, 
        string $cacheName, 
        File $file, 
        string $targetPath, 
        Image $imageObject
    ): ?string
    {
        // Return the path to a custom image
        if (…) {
            return $newImagePath;
        }

        return null;
    }
}
```


## References

* [\Contao\CoreBundle\Image\LegacyResizer#L100-L114](https://github.com/contao/contao/blob/4.7.6/core-bundle/src/Image/LegacyResizer.php#L100-L114)
