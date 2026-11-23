# mia_pretraining

Dataset dashboard and training approval tracker for LMVD pretraining data.

One issue per dataset (or crop) in the data collection `/groups/miaai/miaai/lmd-v0.0.1/`. Annotation and proofreading of the data, and the labels ingested into it, are tracked in [mia_annotation](https://github.com/AI-HHMI/mia_annotation).

**Project board**: https://github.com/orgs/AI-HHMI/projects/4/views/1

## 1. Add a dataset or a crop: use the form

Open the form directly: **https://github.com/AI-HHMI/mia_pretraining/issues/new?template=data_ingestion.yml** (or the list of forms at https://github.com/AI-HHMI/mia_pretraining/issues/new/choose, or **Issues** > **New issue**). **New issue** offers the form **Add a dataset or a crop to the data collection**. Go through the steps in order (Step 1, Step 2, ...), fill the required ones (a step marked *optional* can stay empty), and submit.

### How to use a form, step by step

1. Open the form at https://github.com/AI-HHMI/mia_pretraining/issues/new?template=data_ingestion.yml (or click **Issues**, then **New issue**).
2. Pick the form from the list and click **Get started**. (A blank issue is still offered at the bottom, but the forms are preferred: the automation reads their answers as written.)
3. Read the short "How this form works" note at the top.
4. Fill the steps in order, Step 1, Step 2, and so on:
   - A step marked **(optional)** can be left empty. Every other step must be filled before you can submit.
   - The grey text in a box shows the format to copy. A dropdown is chosen from its list.
   - Keep the formats exactly (boxes as `Z[start:end], Y[start:end], X[start:end]`, links and paths, `@` before a GitHub user), because the automation reads them.
5. Click **Submit new issue**. The issue is written from your answers, under one heading per step.
6. Then use comments as before, and answer the automation when it asks a question on the issue.
7. If you made a mistake, edit the issue (**...** then **Edit**) or add a comment with the correction; do not open a second issue for the same request.

What each step asks for:

| Steps | What you give |
|---|---|
| 1 to 2 | what is new (a new dataset, a new crop of an existing one, or a volume that replaces an earlier dataset) and the dataset issue it belongs to or replaces |
| 3 to 8 | the dataset: project, organism, modality, name, source type (internal or external) and source lab. They match the board fields of the same names |
| 9 to 12 | the source: cluster path, format and size, voxel size (only if the file does not say it), expansion factor and who confirmed it |
| 13 to 14 | the crop: a Neuroglancer link to the box, or `Z[a:b], Y[a:b], X[a:b]` with the grid; the crop name |
| 15 to 22 | the labels that come with the data (leave empty when there are none): where they are, what they segment (cell, neuron, nucleus, mitochondria, ...), instance or semantic, where they come from (manual, automatic prediction, proofread, public), how much they cover, the class table of a semantic label, who made them and when |
| 23 to 24 | license (CC BY 4.0 for Janelia data, another public license, or not stated at the source) and publication |
| 25 to 26 | who to hand it to, and notes |

## 2. What happens next

The volume and the box are checked, and a findings comment on the issue states what will be ingested (dataset, crops, labels, license). After the approver has checked it and says yes, the data is written into the data collection, the crop is checked, the board fields are filled and the issue is linked to its label issues in mia_annotation. A problem (a name that is already taken, a box outside the volume, a source that cannot be read) is asked about on the issue; nothing is overwritten without an answer. A crop or a dataset folder is never replaced: a taken name is answered with `/rename`.

## 3. Status

`Pending Ingestion` (waits for the data to be ingested), `Training Bbox TBD`, `Waiting`, `Consider for Training`, `Approved for Training`, `In Training`, `Model Development Only`, `On Hold`, `Discarded` (with `Discard_Reason`).

## 4. Board fields

The board describes each dataset: `Organism`, `Data_Modality`, `Source_Type` (Internal (Janelia/HHMI), External (Public), External (Collaboration)), `Source_Lab`, the paths (`Raw_Source_Path`, `HHMI_Path`, `Fileglancer_Path`, `Label_Path`), the shape of the data (`Voxel_Size_ZYX_nm`, `Volume_Shape_ZYX`, `Physical_Volume`, `Array_Dims`, `Axis_Order`, `Dtype`, `Disk_Size`), how it is stored (`Zarr_Format`, `Chunk_Shape`, `Shard_Shape`, `Compression`, `Num_Scales`), what it holds (`Structure`, `Has_Seg`, `Label_Description`, `Expansion_Factor`, `Pct_Nonzero`), the source paper (`Paper_DOI`) and the training box (`Training_BBox_s0_zyx`).
