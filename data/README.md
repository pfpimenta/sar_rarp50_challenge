# SAR-RARP50

The SAR-RARP50 dataset provides surgical video of the DVC phase from 50 different
real RARP operations. Each video file is accompanied by surgical gesture annotations
at 10Hz and surgical instrumentation masks at 1Hz.
This dataset and accompanying files are licensed under a [Creative Commons
Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)] (https://creativecommons.org/licenses/by-nc-sa/4.0/).

## Dataset Format

The dataset is provided as a collection of video subfolders, each corresponding to a different RARP operation.
The file structure of a video subfolder is as follows:

```tree
video_xx/
├── segmentation/
│   ├── 000000000.png
│   ├── 000000060.png
│   ├── ...
│   └── xxxyyyzzz.png
├── action_continuous.txt
├── action_discrete.txt
└── video_left.avi
```

- `video_left.avi` is the left endoscopic video channel of the stereo endoscope.
The video was captured at 60Hz at 1080i resolution, then it was de-interlaced and
time-synchronized with the right stereo video channel. The time synchronization process
 may have introduced duplicate frames in the provided video file. The provided video
is re-encoded at a constant FPS of 60.
- `action_continuous.txt` contains action annotations in a continuous format. The has a CSV
format, with the first column indicating the frame the gesture starts from, the second column indicating the frame the gesture ends at and the third indicates the class of the gesture.
- `action_discrete.txt` contains action annotations in a discrete frame-by-frame format
at 10Hz. The file has a CSV format with every row corresponding to a specific frame in the
video. The first column indicates the frame number of `video_left.avi` and the second,
the class of the gesture.
- `segmentation/` is a directory containing instrumentation semantic segmentation masks
for video frames sampled at 1Hz. Each segmentation mask is a grayscale PNG image with the same
resolution as the video. The file name of each segmentation mask corresponds to the frame
number of the video frame it was generated from. For example, the segmentation mask
`000000060.png` corresponds to frame 60 of the corresponding `video_left.avi`. The
grayscale value of each pixel in the segmentation mask corresponds to the class of
the instrument in that pixel.
We provide a Python script that extracts frames at 10Hz from `video_left.avi` and places
them in a directory called `frames/`adjacent to the video file.

### Action Recognition dictionary

The third column of the `action_continuous.txt` and the second column of the `action_discrete.txt`
correspond to action labels in numeric format. The following table describes the mapping between
each class number and the corresponding action label in text form.
| RGB value | Segmentation class                    |
|-----------|---------------------------------------|
| 1         | Other                                 |
| 2         | Picking-up the needle                 |
| 3         | Positioning the needle tip            |
| 4         | Pushing the needle through the tissue |
| 5         | Pulling the needle out of the tissue  |
| 6         | Tying a knot                          |
| 7         | Cutting the suture                    |
| 8         | Returning/dropping the needle         |

### Segmentation masks format

segmentation masks are provided as .png images at the same resolution as the original video frames.
The grayscale value of each pixel corresponds to a semantic class. The mapping between grayscale pixel
values and semantic labels in text form is described in the following table.
| RGB value | Segmentation class |
|-----------|--------------------|
| 0         | Background         |
| 1         | Tool clasper       |
| 2         | Tool wrist         |
| 3         | Tool shaft         |
| 4         | Suturing needle    |
| 5         | Thread             |
| 6         | Suction tool       |
| 7         | Needle Holder      |
| 8         | Clamps             |
| 9         | Catheter           |

### Challenge Dataset split

During the challenge,  the dataset was released in three parts:
- Training set 1 (13 operations): videos 2, 4, 5, 6, 8, 9, 10, 11, 12, 15, 16, 17, 19
- Training set 2 (27 operations): videos 1, 3, 7, 13, 18, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 34, 33, 34, 35, 36, 37, 38, 39, 40
- Test set (10 operations): videos 41, 42, 43, 44, 45, 46, 47, 48, 49, 50
Videos 11, 15, 17 and 29, are split into two parts and annotated as video_xx_1 and video_xx_2.
Such operations are treated as one during evaluation and we recommend to be used as one dataset
when training action recognition models.