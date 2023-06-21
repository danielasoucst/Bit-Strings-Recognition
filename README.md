# Bit-Strings-Recognition
## Using YOLO Network for Automatic Processing of Finite Automata Images with Application to Bit-Strings Recognition (DocEng 2023)

**Dependencies**

    - Pytorch
    
    - keras-ocr
    
    - pytesseract
    
    - OpenCV
    
    - Skimage
    
    - Numpy
    
**Clone darnet git repository:**    

`!git clone https://github.com/AlexeyAB/darknet`

**Download the pre-trained *`yolov4`* weights**
`!wget https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v3_optimal/yolov4.conv.137`

**Create obj.data, obj_test.data and obj.names:**

```
import re
objdata =  '/darknet/data/obj.data'

#the number of classes is equal to the number of labels
num_classes = 5

with open(objdata, 'w') as f:
  f.write(f"classes = {num_classes}\n")
  f.write(f"train = data/train.txt\n")
  f.write(f"valid = data/validation.txt\n") 
  f.write(f"names = data/obj.names\n")
  f.write(f"backup = /training")
```

```
import re
objdata = '/darknet/data/obj_test.data'

#the number of classes is equal to the number of labels
num_classes = 5   

with open(objdata, 'w') as f:
  f.write(f"classes = {num_classes}\n")
  f.write(f"train = data/train.txt\n")
  f.write(f"valid =  data/test.txt\n") 
  f.write(f"names =  data/obj.names\n")
  f.write(f"backup =  //training")
```

```
labels_path = 'obj.names'

# make a list of your labels
filter_categories = ['state', 'final state', 'arrow', 'label', 'arrow_in']
labels = filter_categories

with open(labels_path, 'w') as f:
    f.write('\n'.join(labels))
```

     
**Link to the model trained on the finite automata dataset (FA):**
  - [yolov4-custom_best.weights](https://drive.google.com/file/d/1ooemXWBQRn9GcELqKGL3PP-XBlGmB27S/view?usp=sharing)
    

**Download datasets**
   - [FA dataset (online)](https://cmp.felk.cvut.cz/~breslmar/finite_automata/)
   - [Mealy Dataset](https://drive.google.com/drive/folders/1uFVDmvQX9JUJBh1ankbBYUGwrRY__FTm?usp=sharing)
     
 **Training and testing**
 
    Train:
    
    `%cd /darknet`
    
    `!./darknet detector train data/obj.data cfg/yolov4-custom.cfg yolov4.conv.137 -dont_show -map`

    Test

    `!./darknet detector map data/obj_test.data cfg/yolov4-custom.cfg /training/yolov4-custom_best.weights -points 0 -iou_thresh 0.8`
    
 **Postprocessing (COLAB link)**
 
In the root directory of Google Drive, create a folder called 'Bit-Strings-Recognition' and paste this notebook: [add link]()


 
    

 
