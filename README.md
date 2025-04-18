# sar_rarp50_challenge
Short attempt to solve a semantic (surgical tool) segmentation task on surgical procedures videos


## SAR-RARP50: Segmentation of surgical instrumentation and Action Recognition on Robot-Assisted Radical Prostatectomy Challenge

The original challenge (https://arxiv.org/pdf/2401.00496) was multimodel, with both multimodal surgical action recognition (frame by frame classification) and semantic instrumentation segmentation (pixel by pixel classification). In this case, only the semantic segmentation task is being addressed.

SAR: Surgical Action Recognition
RARP: Robotic Assisted Radical Prostatectomy

* Background information: the exercise focuses on surgical tool segmentation, which is crucial in various computer-assisted intervention applications. This task involves processing RGB video frames and assigning semantic labels at the pixel level.
* Goal: your objective is to solve the semantic segmentation task and generate masks of prominent objects, including surgical tool parts, as well as thin and small tools such as surgical clips, suturing threads, and needles.
* Data, you can access the training and test sets using the following links (for more information see https://www.synapse.org/#!Synapse:syn27618412/wiki/616881)
    - Train set: https://rdr.ucl.ac.uk/articles/dataset/SAR-RARP50_train_set/24932529
    - Test set: https://rdr.ucl.ac.uk/articles/dataset/SAR-RARP50_test_set/24932499
* Submission requirements, please submit the following via email:
    - Code: attach a zip file containing your code to your response email and provide a link to a GitHub repository where your code is stored.
    - Report: attach a PDF file containing your report (including details of your method, evaluation protocol, and results). Additionally, provide a link to an Overleaf project with your report.
* Deadline: the deadline for submitting both the code and report is Sunday, Apr 20th, at 4:00 GMT.

-------------------------

## Notes

* Task: processing RGB video frames and assigning semantic labels at the pixel level.

input: (time_frames, width, height, channel)
output: (time_frames, width, height)

