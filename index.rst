..
  Technote content.

  See https://developer.lsst.io/restructuredtext/style.html
  for a guide to reStructuredText writing.

  Do not put the title, authors or other metadata in this document;
  those are automatically added.

  Use the following syntax for sections:

  Sections
  ========

  and

  Subsections
  -----------

  and

  Subsubsections
  ^^^^^^^^^^^^^^

  To add images, add the image file (png, svg or jpeg preferred) to the
  _static/ directory. The reST syntax for adding the image is

  .. figure:: /_static/filename.ext
     :name: fig-label

     Caption text.

   Run: ``make html`` and ``open _build/html/index.html`` to preview your work.
   See the README at https://github.com/lsst-sqre/lsst-technote-bootstrap or
   this repo's README for more info.

   Feel free to delete this instructional comment.

:tocdepth: 1

.. Please do not modify tocdepth; will be fixed when a new Sphinx theme is shipped.

.. sectnum::

.. TODO: Delete the note below before merging new content to the master branch.

.. note::

   **This technote is not yet published.**

   Plan of the upgrade of the Tucson test stand

.. Add content here.
.. Do not include the document title (it's automatically added from metadata.yaml).

Storage
=======

Storage for the TTS is spread across the Kubernetes (pillan) cluster and the bare metal machines supporting application deployment.
The sections below will break down the needs for each component.

Kubernetes
----------

The Kubernetes storage provides three categories: block, CephFS/NFS and LFA (S3) storage. Block storage handles the needs of the Kubernetes nodes for image storage.
CephFS/NFS storage handles Nublado storage, pods requesting persistent volumes and CSC pre-cache information.
LFA storage handles CSC and ancillary data not designed to fit within the Engineering Facilities Database (EFD).

For the block storage, the need is largely driven by Docker image storage on the nodes.
The images are combined from SQuaRE services and T&S and DM CSCs and services.
A storage size of 30 TB should handle the needs of the image storage.

For the CephFS/NFS storage, the need is driven by CSC pre-cache information, which has grown over since the TTS was first envisioned.
Nublado usage of this storage based on current summit numbers amounts to about 5 TBs.
Factoring in the current expansion of CSC pre-cache information and possible expansion of Nublado use, a storage size of 30 TB should fit the needs of this category.

For the LFA storage, the need is driven by having a 30 day store for ComCam.
This requires approximately 20 TBs for about 5000 images per day.
A comparable 30 day store for AuxTel is approximately 2 TBs.
Factoring in the unknown expansion use by other systems running on TTS and adding overhead, the LFA should contain 50 TBs of storage.
Removal of older files should be enforced if there is pressure on the storage as the data is considered expendable.

Bare Metal Machines
-------------------

The following machines have a 2 TB NVMe drive and a 1 TB SSD drive.

  * `love1`
  * `tel-hw1`
  * `auxtel-mcm`
  * `auxtel-fp01`
  * `auxtel-archiver`
  * `comcam-mcm`
  * `daq-mgt`

The following machines have a 2 TB NVMe drive and a 500 GB SSD drive.

  * `comcam-fp01`
  * `comcam-dc01`
  * `comcam-archiver`
  * `forwarders`

The `comcam-archiver` machine has an additional 16 TBs of SSDs under a RAID controller.
The `daq-mgt` machine has an additional 2 TB NVMe drive.

The storage needs for the bare metal machines are governed by the applications that run on those systems.
The system principles responsible for the machines have determined that the currently available storage is sufficient for their needs.


.. .. rubric:: References

.. Make in-text citations with: :cite:`bibkey`.

.. .. bibliography:: local.bib lsstbib/books.bib lsstbib/lsst.bib lsstbib/lsst-dm.bib lsstbib/refs.bib lsstbib/refs_ads.bib
..    :style: lsst_aa
