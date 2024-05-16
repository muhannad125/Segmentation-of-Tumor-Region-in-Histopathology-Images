<a name="readme-top"></a>

## Table of Contents
<!-- TABLE OF CONTENTS -->
  <ol>
    <li>
      <a href="#About the Project">About The Project</a>
    </li>
    <li>
      <a href="#Proposed Pipeline">Proposed Pipeline</a>
    </li>
    <li><a href="#Handling the Imbalance in the Training Dataset">Handling the Imbalance in the Training Dataset</a></li>
    <li><a href="#Results">Results</a>
      <ul>
        <li><a href="# Evaluation of CNN Performance">Evaluation of CNN Performance</a></li>
        <li><a href="# Evaluation of U-Net Performance">Evaluation of U-Net Performance</a></li>
      </ul>
    </li>
    <li><a href="#Examples">Examples</a>
  </ol>

## About the Project

This project examines the segmentation of tumor patches within whole-slide images (WSI) and presents the findings from 3 different modeling approaches; CNN and ResNet as binary classifiers, and U-net architecture for segmentation tasks. While the U-net design creates a binary mask characterizing the tumor locations, the CNN architecture provides a binary output showing the presence or absence of tumors in a specific patch.


## Proposed Pipeline
<figure style="display: block; text-align: center;">
  <img  src="https://github.com/muhannad125/cancer_segmentation/assets/61150919/1d9dc881-f699-4967-82d4-3c45fa87a834" alt="Image" style="display: block; margin: 0 auto;width: 50%;">
  <br>
  <figcaption style="margin-top: 5px;"><em>Figure 1: Block Schema of The Proposed Pipeline.</em></figcaption>
</figure>

<br>
<br>
Given the high-resolution nature of WSI images, they are typically too large to be directly input into a model. Consequently, the proposed pipeline is as shown in the Figure , WSIs are divided into smaller images (256x256 pixels) called patches, along with corresponding mask images that indicate the viable tumor area. These mask patches serve as the ground truth for tumor regions. The generated patches are then given to an AI Model to be trained. The AI architecture used in this project can be U-net for pixel-wise classification, CNN and ResNet for patch-wise classification. The results of both models are then evaluated using several metrics such as IoU and F1-score.

## Dataset Design
Patches that have less than 80% cancerous area are considered Partially tumorous.
<figure style="display: block; text-align: center;">
  <img  src="https://github.com/muhannad125/cancer_segmentation/assets/61150919/71621529-e1ee-4bda-b42e-ceb6b7dcaed7" alt="Image" style="display: block; margin: 0 auto;width: 50%;">
  <br>
  <figcaption style="margin-top: 5px;"><em>Figure 2.0: Patched Image Examples.</em></figcaption>
</figure>
<br>
<br>


<figure style="display: block; text-align: center;">
  <img  src="https://github.com/muhannad125/cancer_segmentation/assets/61150919/7aeecdeb-71c9-413f-9cdd-a61fe1078f91" alt="Image" style="display: block; margin: 0 auto;width: 50%;">
  <br>
  <figcaption style="margin-top: 5px;"><em>Figure 2.1: WSI Image.</em></figcaption>
</figure>
<br>

## Handling the Imbalance in the Training Dataset
In the training dataset, there is a noticeable imbalance between the number of noncancerous patches and cancerous ones. This imbalance may adversely affect the training process, as the model may become biased towards the majority class (noncancerous patches) and might not perform well in identifying the minority class (cancerous patches). This issue could lead to a higher false-negative rate, which is not desirable in medical applications where accurate detection of cancerous regions is crucial.
To mitigate the effects of this class imbalance, several techniques is used for both pixel-wise segmentation and patch-wise classification tasks.

## Results
The CNN and U-Net models were trained on 2 different amount of data: 20 WSIs and 45 WSIs. In this case, it is an expected result that the success will increase with the increase in the number of data. However, the increase in the amount of data made the test and train processes more recourse consuming in terms of time and hardware.


### Evaluation of CNN Architecture Performance
<figure style="display: block; text-align: center;">
  <img  src="https://github.com/muhannad125/cancer_segmentation/assets/61150919/3d856356-e2f1-491e-9d8d-1470e0b5b9e1" alt="Image" style="display: block; margin: 0 auto;width: 75%;">
  <br>
  <figcaption style="margin-top: 5px;"><em>Figure 3.0: Results of CNN trained on 20 WSI (Partially Tumorous patches labeled as Tumorous)
</em></figcaption>
</figure>
<br>
<br>


<figure style="display: block; text-align: center;">
  <img  src="https://github.com/muhannad125/cancer_segmentation/assets/61150919/169b7c1d-72a2-4e6f-a8e6-0866c6c344b9" alt="Image" style="display: block; margin: 0 auto;width: 75%;">
  <br>
  <figcaption style="margin-top: 5px;"><em>Figure 3.1: Results of CNN trained on 20 WSI (Partially Tumorous patches labeled as Non-Tumorous)
</em></figcaption>
</figure>
<br>
<br>



<figure style="display: block; text-align: center;">
  <img  src="https://github.com/muhannad125/cancer_segmentation/assets/61150919/e79a6755-942e-452e-ad4e-360bb3879498" alt="Image" style="display: block; margin: 0 auto;width: 75%;">
  <br>
  <figcaption style="margin-top: 5px;"><em>Figure 3.2: Results of CNN trained on 45 WSI (Partially Tumorous patches labeled as Tumorous)

</em></figcaption>
</figure>
<br>
<br>

### Evaluation of U-Net Performance
It has been observed that training the models on WSIs with a balanced distribution give better performance. The reason for this is that the models trained on unbalanced distributions have a chance to overfit, resulting in bad performance.

Different distributions and data size were tested to find the best performing model. As shown in the Figure 3.3 and Figure 3.5 when training U-net on only cancerous data the model becomes overfitted towards cancerous data resulting in 0 accuracy on benign data.
Also, Figure 3.5 shows that when training U-Net on 45 WSIs with 50% benign and 50% malignant data the model becomes biased towards benign data. This can be because of the huge amount of benign patches in the 45 WSIs. It is crucial for U-net to balance the data used for training in order to get satisfying results.

<figure style="display: block; text-align: center;">
  <img  src="https://github.com/muhannad125/cancer_segmentation/assets/61150919/45decf06-8f95-4441-99dc-b2a8abdbb648" alt="Image" style="display: block; margin: 0 auto;">
  <br>
  <figcaption style="margin-top: 5px;"><em>Figure 3.3: Results of U-Net trained on 20 Whole Slide Images (WSIs).

</em></figcaption>
</figure>
<br>
<br>

<figure style="display: block; text-align: center;">
  <img  src="https://github.com/muhannad125/cancer_segmentation/assets/61150919/0392a433-6935-4d59-aa50-b356b564ac0e" alt="Image" style="display: block; margin: 0 auto;width:50%">
  <br>
  <figcaption style="margin-top: 5px;"><em>Figure 3.4: Over all results of the U-net trained on 20 WSI

</em></figcaption>
</figure>
<br>
<br>

<figure style="display: block; text-align: center;">
  <img  src="https://github.com/muhannad125/cancer_segmentation/assets/61150919/4ef9d5ec-bd47-4ece-95ca-f4d9ec2f627b" alt="Image" style="display: block; margin: 0 auto;">
  <br>
  <figcaption style="margin-top: 5px;"><em>Figure 3.5: Results of U-Net trained on 45 Whole Slide Images (WSIs).

</em></figcaption>
</figure>
<br>
<br>

<figure style="display: block; text-align: center;">
  <img  src="https://github.com/muhannad125/cancer_segmentation/assets/61150919/134ea6f2-449b-4fd3-9f24-75250315fb4b" alt="Image" style="display: block; margin: 0 auto;width:50%">
  <br>
  <figcaption style="margin-top: 5px;"><em>Figure 3.6: Over all results of the models trained on 45 WSI

</em></figcaption>
</figure>
<br>
<br>


## Examples

<figure style="display: block; text-align: center;">
  <img  src="https://github.com/muhannad125/cancer_segmentation/assets/61150919/fdae55bb-31cd-428e-bcf7-d2e927381603" alt="Image" style="display: block; margin: 0 auto;">
  <br>
  <figcaption style="margin-top: 5px;"><em>Figure 4.0: Example results of the trained models Model 1*: Best performing U-Net model trained on 20 WSI Model 2*: Best performing U-Net model trained on 45 WSI
</em></figcaption>
</figure>
<br>
<br>

<figure style="display: block; text-align: center;">
  <img  src="https://github.com/muhannad125/cancer_segmentation/assets/61150919/437570bc-a12d-4bd7-8d7d-8a99d765e8b9" alt="Image" style="display: block; margin: 0 auto;width:50%">
  <br>
  <figcaption style="margin-top: 5px;"><em>Figure 4.1: Segmentation of Training_phase_2_048
</em></figcaption>
</figure>
<br>
<br>
 

<figure style="display: block; text-align: center;">
  <img  src="https://github.com/muhannad125/cancer_segmentation/assets/61150919/65963555-7b32-421e-ad86-c33701ff361a" alt="Image" style="display: block; margin: 0 auto;width:50%">
  <br>
  <figcaption style="margin-top: 5px;"><em>Figure 4.2: Segmentation of Training_phase_2_050
</em></figcaption>
</figure>
<br>
<br>

## Contirbuters
<!-- CONTACT -->
## Contributors

Muhannad Tuameh - muhannadtumah@gmail.com

Emre Arslanoğlu - emre.arslanoglu@std.yildiz.edu.tr

Project Link: [https://github.com/muhannad125/cancer_segmentation](https://github.com/muhannad125/cancer_segmentation)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

