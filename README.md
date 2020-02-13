# CT DICOM Images

1. classify a folder of DICOM images(even with subfolders) by 4-level hierachy `patient/study/series/instance`.  

   It's inspired from [The Structure of DICOMDIR](https://www.medicalconnections.co.uk/kb/DICOMDIR/) and [Read DICOM directory](https://pydicom.github.io/pydicom/stable/auto_examples/input_output/plot_read_dicom_directory.html#sphx-glr-auto-examples-input-output-plot-read-dicom-directory-py).

   **Note:** In pydicom V1.4, it does not support to create DICOMDIR file and the feature will be introduced in future 2.0 version. The example of reading DICOMDIR uses the file which is generated by `dcmtk`. 

2. organize the classified DICOM images as tree view.

   use PySimpleGUI - tkinter to show tree view.



PySimpleGUI - tkinter version:
[PySimpleGUI](https://github.com/PySimpleGUI/PySimpleGUI)
[Tree Element](https://github.com/PySimpleGUI/PySimpleGUI#tree-element)

QT QML Treeview:
[Tutorial Qt Creator - QML - TreeView](https://www.youtube.com/watch?v=J_jMDro3sMg)
[empty TreeView in QML from jsonModel](https://github.com/eyllanesc/stackoverflow/tree/master/questions/50007170)
[TreeModelFromJSONApp](https://gitlab.com/eska2000/TreeModelFromJSONApp)
[QML TreeView](https://ruedigergad.com/2011/08/14/qml-treeview/)
[Create Model for QML TreeView](https://stackoverflow.com/questions/45166367/create-model-for-qml-treeview)
[Qt qml treeview 树控件](https://www.cnblogs.com/surfsky/p/4309299.html)
[QML自定义树控件（TreeView 的style加上节点可拖动）](https://blog.csdn.net/weixin_40912639/article/details/83962250)
QT QWidget Treeview:
[PyQt5 Treeview](https://pythonspot.com/pyqt5-treeview/)

## Usage

Requirement: Python3.6+

```sh
pip install -r requirements.txt
python app.py
```

## DICOM CT Images Sorting

How the DICOM CT images should be sorted is ultimately dependent on the usage context, but as a rule of thumb I would recommend that you first group the images based on (patient), study and series using these tags:

```sh
(0010,0020)  Patient ID
(0020,000D)  Study Instance UID
(0020,000E)  Series Instance UID
```

To sort the images within one series, you could use the Instance Number (0020,0013), although there is no guarantee that this value is set since it is a type 2 attribute.

Another alternative is to use the Image Position (Patient) (0020,0032), which is mandatory in CT images. You would need to check the Image Orientation (Patient) (0020,0037) to decide how to sort on position. Often CT image orientation is (1,0,0), (0,1,0), and then the Z (third) component of the image position can be used as the basis for sorting.

If the series also contains a localizer image, this image would have to be excluded from positional sorting.

