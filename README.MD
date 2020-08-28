
## About

dcm_qa_canon is a simple DICOM to NIfTI validator script and dataset to test conversion of Canon (né Toshiba) diffusion tensor imaging. Specifically, to ensure that the DICOM gradient vector direction are transformed to match the FSL standard. Note that different vendors use [different conventions](https://www.na-mic.org/wiki/NAMIC_Wiki:DTI:DICOM_for_DWI_and_DTI) to report gradient directions. The goal is to convert these to [FSL's bvec format](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FDT/FAQ#What_conventions_do_the_bvecs_use.3F) which is in [image space](http://justinblaber.org/brief-introduction-to-dwmri/).


The images were acquired on a Canon Galan 3T by Clément Debacker at Le Groupe Hospitalier Universitaire Paris. 

Inspection of the DICOM header tags reveals that these images do not [report diffusion gradients in typical tags](https://www.na-mic.org/wiki/NAMIC_Wiki:DTI:DICOM_for_DWI_and_DTI). Rather, the gradient direction is inserted into the [image comments](http://dicomlookup.com/lookup.asp?sw=Tnumber&q=(0020,4000)) field. The gradient orientation appears to reflect coordinates with respect to the scanner bore (like Siemens, Philips and UIH), rather than the image space (like GE):

```
 (0018,9087) FD 1500                                     #   8, 1 DiffusionBValue
 (0020,4000) LT [b=1500(0.445,0.000,0.895)]              #  26, 1 ImageComments
```

The provided dataset adjust the acquisition orientation (axial, coronal, sagittal) and the image angulation. The rationale is to identify whether an image-space or world-space frame of reference is used, and to ensure that these are accurately transformed to FSL's image space format. A [dedicated document](https://www.nitrc.org/plugins/mwiki/index.php/dcm2nii:MainPage#Diffusion_Tensor_Imaging) describes this procedure.


## Series

* 12000_DTI_ortho
  * Description: Axial acquisition with no angulation (image space aligned to world). space).

* 13000_DTI_SAG_20d
  *  Description: Sagittal acquisition with 20-degree angulation.

* 14000_DTI_AX_20d
  * Description: Axial acquisition with with 20-degree angulation.

* 15000_DTI_COR_20d
  * Description: Coronal acquisition with with 20-degree angulation.

* 16000_DTI_ALL_20d
  *  Description: Sagittal acquisition with 20-degree angulation in each dimension (yaw, pitch, roll).
 