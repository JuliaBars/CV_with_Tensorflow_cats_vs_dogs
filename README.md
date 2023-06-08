
## Сверточная нейронная сеть для классификации изображений:
#### 1 вариант ~ 70% точности
-  [ссылка на модель 1](https://github.com/JuliaBars/CV_with_Tensorflow_cats_vs_dogs/blob/main/models/1_CNN.ipynb)
#### 2 вариант ~ 85% точности (добавление data augmentation) 
- [ссылка на модель 2](https://github.com/JuliaBars/CV_with_Tensorflow_cats_vs_dogs/blob/main/models/2_CNN_data_augmentation.ipynb)
#### 3 вариант ~ 97% точности (переиспользование предварительно обученной модели) 
- [ссылка на модель 3](https://github.com/JuliaBars/CV_with_Tensorflow_cats_vs_dogs/blob/main/models/4_CNN_with_VGG16_freeze.ipynb)

---
---
Для обучения моделей использовался сервис **Google Colaboratory**.

---

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white) ![Colab](https://img.shields.io/badge/google_colaboratory-F9AB00?style=for-the-badge&logo=google-colab&logoColor=white)

---
##### Как загрузить и обработать данные для обучения моделей с Kaggle

Для загрузки dataset с Kaggle необходимо быть там зарегистрированным, 
в разделе настройки профиля выбрать API -> Create new token, JSON файл загрузится на ваш компьютер.
Загрузить этот файл на Colab:
```
from google.colab import files
files.upload()
```
Создать папку и настроить права:
```
!mkdir ~/.kaggle
!cp kaggle.json ~/.kaggle/
!chmod 600 ~/.kaggle/kaggle.json
```

Скачать dataset и распаковать:
```
!kaggle competitions download -c dogs-vs-cats
!unzip -qq train.zip
```
Далее выполните код из листинга, для создания нужных директорий с обучающими, тестовыми и контрольными данными:
```
import os, shutil, pathlib

original_dir = pathlib.Path('train')
new_base_dir = pathlib.Path('cats_vs_dogs_small')

def make_subset(subset_name, start_index, end_index):
  for category in ('cat', 'dog'):
    dir = new_base_dir / subset_name / category
    os.makedirs(dir)
    fnames = [f"{category}.{i}.jpg" for i in range(start_index, end_index)]
    for fname in fnames:
      shutil.copyfile(src=original_dir / fname, dst=dir / fname)

make_subset('train', start_index=0, end_index=1000)
make_subset('validation', start_index=1000, end_index=1500)
make_subset('test', start_index=1500, end_index=2500)
```
---


_автор Юлия Орлова_
_Репозиторий на Github [ссылка](https://github.com/JuliaBars/CV_with_Tensorflow_cats_vs_dogs)._
