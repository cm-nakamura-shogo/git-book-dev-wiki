# Augmentation

## SMOTE

- https://www.ibm.com/blogs/solutions/jp-ja/spssmodeler-push-node-10/

## Keras ImageDataGenerator 

- [Keras - Keras の ImageDataGenerator を使って学習画像を増やす - Pynote](https://pynote.hatenablog.com/entry/keras-image-data-generator)

## Albumentations

こちらも画像の変換が可能なライブラリ

- [GitHub](https://github.com/albumentations-team/albumentations)

## Random Erasing
  
- https://qiita.com/takurooo/items/a3cba475a3db2c7272fe

## mixup

- 新しめの例（しかし単体の実装例
  - https://tensorflow.classcat.com/2021/12/01/keras-2-examples-vision-mixup/
- そもそもImageDataGeneratorとは
  - https://www.tensorflow.org/api_docs/python/tf/keras/preprocessing/image/ImageDataGenerator
- ImageDataGeneratorを拡張実装例あり（参考になるものの、いくつか疑問のある実装...）
  - https://qiita.com/koshian2/items/909360f50e3dd5922f32
- ImageDataGeneratorを拡張した実装例２（こっちの方が今見ると筋がいい実装）
  - https://maxigundan.com/deeplearning/2020/04/%E3%80%90tf2%E3%80%91imagedatagenerator%[…]%9Caugmentation%E6%A9%9F%E8%83%BD%E3%82%92%E8%BF%BD%E5%8A%A0/
- mixup単体の実装例
  - https://qiita.com/yu4u/items/70aa007346ec73b7ff05
- keras公式のmixup。one_hotの部分は参考にした。
  - https://keras.io/examples/vision/mixup/
- mixupの理論
  - https://wazalabo.com/mixup_1.html