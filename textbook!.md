---
title: scan this picture and index the whole video/document/ppt/textbook!
created: '2022-08-24T16:02:15.000Z'
modified: '2022-08-25T09:58:03.255Z'
---

# scan this picture and index the whole video/document/ppt/textbook!

## kindly reminders

when building python c++ libraries without xcode, please add commandline header files like this:

in order to have this during build:
```/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.8/Headers/Python.h```

we need to do:
```bash
ln -s /Library/Developer/CommandLineTools /Applications/Xcode.app/Contents/Developer
```

## search by image instead of cranking latex out

### image search libraries

character level optical char segmentation called [chargrid ocr](https://github.com/akkshita/chargrid-ocr)

[image match used for copyright violation detection, using phash algorithm](https://github.com/ProvenanceLabs/image-match)

## get the latex out

### first detect the location of math formula

[scanning single shot detection for math formulas](https://github.com/MaliParag/ScanSSD)

[dataset for math symbol detection](https://github.com/MaliParag/TFD-ICDAR2019)

[detect different part of document with yolov3](https://github.com/Binhhp/detector-scan-image)

[math expression detection](https://github.com/divya1211/math-expression-detection)

### next find the tool for picture to latex conversion

[deeplearning picture to latex](https://github.com/kingyiusuen/image-to-latex)

[pix2tex](https://github.com/lukas-blecher/LaTeX-OCR)

[using pix2tex](https://pix2tex.readthedocs.io/en/latest/pix2tex.html#pix2tex-api-package)

[中文公式 手写公式识别 需要进一步训练](https://github.com/LinXueyuanStdio/LaTeX_OCR_PRO)

[中文 手写 pytorch版本](https://github.com/qs956/Latex_OCR_Pytorch)

## mask latex area and get conventional things out

[easyocr with pytorch support](https://github.com/JaidedAI/EasyOCR)

## search the formula

[formula search based on sympy](https://github.com/AzizAlqasem/FormulaLab)

can we render latex to picture with sympy?

[latex search engine](https://github.com/kerryz/latexsymbolsearch)
