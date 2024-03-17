---
author: John
tags: programming os
---

Tried powershell once and you will fall in love with it.

Before trying: why on earth do we need another shell script language?
After: Fuck it's so .. powerful, for the following reasons:

1. Object-Oriented, which makes your script highly readable and maintainable.
2. More functions are supported, like picture processing.
3. It's advanced. Supporting advanced feature like modules.
4. It's easy to learn. You can even execute alias command like `ls`.

Here's a simple picture preview app I wrote in Powershell:
![pic](/assets/img/posts-202403/03-powershell.png)

It can display specified image in console, for example this is the original
image that it displayed:
![pic](/assets/img/posts-202403/03-supermario.jpeg)

the powershell snippet I wrote for it:

```powershell
function Show-Image {
    param (
        [String] $Path
    )
    $bmp = [System.Drawing.Bitmap]::FromFile($Path)
    foreach($y in 1..($bmp.height-1))
    {
        foreach($x in 1..($bmp.width-1)){
            $pixel = $bmp.GetPixel($x, $y)
            $value = ($pixel.R + $pixel.G + $pixel.B) * 1.3
            if ($value -gt 768) {
                $color = 'white'
            } elseif ($value -gt 512) {
                $color = 'gray'
            } elseif ($value -gt 256) {
                $color = 'darkgray'
            } else {
                $color = 'black'
            }
            Write-Host -BackgroundColor $color -NoNewline '  '
        }
        Write-Host ''
    }

}
```
