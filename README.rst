********
omop2obo
********

|logo|

|pip| |downloads|

|github_action|  |ABRA|

|sonar_quality| |code_climate_maintainability| |sonar_maintainability| |coveralls| |code_climate_coverage|

|

What is OMOP2OBO?
#################

``omop2obo`` is a collection of health system-wide, disease-agnostic mappings between standardized clinical terminologies in the Observational Medical Outcomes Partnership (`OMOP`_) common data model and several Open Biomedical Ontologies (`OBOs`_) foundry ontologies.

*Motivation*

Common data models have solved many challenges of utilizing electronic health records, but have not yet meaningfully integrated clinical and molecular data. Aligning clinical data to open biological ontologies (`OBOs`_), which provide semantically computable representations of biological knowledge, requires extensive manual curation and expertise.

*Objective*

To address these limitations, we have developed ``OMOP2OBO``, the first health system-wide integration and alignment between the Observational Health Data Sciences and Informatics' Observational Medical Outcomes Partnership (`OMOP`_) standardized clinical terminologies and eight OBO biomedical ontologies spanning diseases, phenotypes, anatomical entities, cell types, organisms, chemicals, metabolites, hormones, vaccines, and proteins. To verify that the mappings are both clinically and biologically meaningful, we have performed extensive experiments to verify the `accuracy <https://github.com/callahantiff/OMOP2OBO/wiki/Accuracy>`__, `generalizability <https://github.com/callahantiff/OMOP2OBO/wiki/Generalizability>`_, and `logical consistency <https://github.com/callahantiff/OMOP2OBO/wiki/Consistency>`_ of each released mapping set.

What Does This Repository Provide?
**********************************

Through this repository we provide the following:

1. **Mappings:** A free set of ``omop2obo`` mappings that can be used out of the box (requires no coding) covering OMOP Conditions, Drug Exposures, and Measurements. These mappings are available in several formats including: ``.txt``, ``.xlsx``, and ``.dump``. We also provide a semantic representation of the mappings, integrated with the OBO biomedical ontologies, available as an edge list (``.txt``) and as an ``.owl`` file. See current release for more details.


2. **A Mapping Framework:** An algorithm and mapping pipeline that enables one to construct their set of `omop2obo` mappings. The figure below provides a high-level overview of the algorithm workflow. The code provided in this repository facilitates all of the automatic steps shown in this figure except for the manual mapping (for now, although we are `currently <https://github.com/callahantiff/OMOP2OBO/issues/19>`__ working on a deep learning model to address this).


How do I Learn More?
********************

- Join an existing or start a new `Discussion`_

- The Project `Wiki`_ for more details on the ``omop2obo`` mappings, algorithm, and information on the experiments we ran to ensure each mapping set released is accurate, generalizable, and consistent!  

- A `Zenodo Community <https://zenodo.org/communities/omop2obo>`__ has been established to provide access to software releases, presentations, and preprints related to this project 

|

Releases
########

- All code and mappings for each release are free to download, see `Wiki <https://github.com/callahantiff/OMOP2OBO/wiki>`__  

- Please see our `dashboard <http://tiffanycallahan.com/OMOP2OBO_Dashboard>`__ to get current stats on available mappings and for links to download them.

|dashboard1| |dashboard2|

**Current Release:** 
 
 - ``v1.0.0`` ➞ data and code can be directly downloaded `here <https://github.com/callahantiff/OMOP2OBO/wiki/V1.0>`__.
 
   - Condition Occurrence Mappings: https://doi.org/10.5281/zenodo.6774363 
   - Drug Exposure Ingredient Mappings: https://doi.org/10.5281/zenodo.6774401 
   - Measurement Mappings: https://doi.org/10.5281/zenodo.6774443


|

Getting Started
###############

Install Library
***************

This program requires Python version 3.6. To install the library from `PyPI <https://pypi.org/project/omop2obo/>`__, run:

.. code:: shell

  pip install omop2obo

|

You can also clone the repository directly from GitHub by running:

.. code:: shell

  git clone https://github.com/callahantiff/OMOP2OBO.git

|

Set-Up Environment
******************

The ``omop2obo`` library requires a specific project directory structure. Please make sure that your project directory includes the following sub-directories:

.. code:: shell

    OMOP2OBO/
        |
        |---- resources/
        |         |
        |     clinical_data/
        |         |
        |     mappings/
        |         |
        |     ontologies/

Results will be output to the ``mappings`` directory.

|

Dependencies
^^^^^^^^^^^^

*APPLICATIONS*

- This software also relies on `OWLTools <https://github.com/owlcollab/owltools>`__. If cloning the repository, the ``owltools`` library file will automatically be included and placed in the correct repository.

-  The National of Library Medicine's Unified Medical Language System (UMLS) `MRCONSO <https://www.nlm.nih.gov/research/umls/licensedcontent/umlsknowledgesources.html>`__ and `MRSTY <https://www.ncbi.nlm.nih.gov/books/NBK9685/table/ch03.Tf/>`_. Using these data requires a license agreement. Note that in order to get the `MRSTY` file you will need to download the UMLS Metathesaurus and run MetamorphoSys. Once both data sources are obtained, please place the files in the ``resources/mappings`` directory.

*DATA*

- **Clinical Data:** This repository assumes that the clinical data that needs mapping has been placed in the ``resources/clinical_data`` repository. Each data source provided in this repository is assumed to have been extracted from the OMOP CDM. An example of what is expected for this input can be found `here <https://github.com/callahantiff/OMOP2OBO/tree/master/resources/clinical_data>`__.

- **Ontology Data:** Ontology data is automatically downloaded from the user provided input file ``ontology_source_list.txt`` (`here <https://github.com/callahantiff/OMOP2OBO/blob/master/resources/ontology_source_list.txt>`__).

- **Vocabulary Source Code Mapping:** To increase the likelihood of capturing existing database cross-references, ``omop2obo`` provides a file that maps different clinical vocabulary source code prefixes between the UMLS, ontologies, and clinical EHR data (i.e. "SNOMED", "SNOMEDCT", "SNOMEDCT_US")  ``source_code_vocab_map.csv`` (`here <https://github.com/callahantiff/OMOP2OBO/blob/master/resources/mappings/source_code_vocab_map.csv>`__). Please note this file builds off of `these <https://www.nlm.nih.gov/research/umls/sourcereleasedocs/index.html>`__ UMLS provided abbreviation mappings. Currently, this file is updated for ontologies released ``july 2020``, clinical data normlaized to ``OMOP_v5.0``, and ``UMLS 2020AA``.

- **Semantic Mapping Representation:**  In order to create a semantic representation of the ``omop2obo`` mappings, an ontological specification for creating classes that span multiple ontologies (``reosurces/mapping_semantics/omop2obo``). This document only needs to be altered if you plan to utilize the semantic mapping transformation algorithm and want to use a different knowledge representation. Please the following `README <https://github.com/callahantiff/OMOP2OBO/tree/master/resources/mapping_semantics/README.md>`__ for additional details on these resources.

|

Running the omop2obo Library
****************************

There are a few ways to run ``omop2obo``. An example workflow is provided below.

.. code:: python

 import glob
 import pandas as pd
 import pickle

 from datetime import date, datetime

 from omop2obo import ConceptAnnotator, OntologyDownloader, OntologyInfoExtractor, SimilarStringFinder


 # set some global variables
 outfile = 'resources/mappings/OMOP2OBO_MAPPED_'
 date_today = '_' + datetime.strftime(datetime.strptime(str(date.today()), '%Y-%m-%d'), '%d%b%Y').upper()

 # download ontologies
 ont = OntologyDownloader('resources/ontology_source_list.txt')
 ont.downloads_data_from_url()

 # process ontologies
 ont_explorer = OntologyInfoExtractor('resources/ontologies', ont.data_files)
 ont_explorer.ontology_processor()

 # create master dictionary of processed ontologies
 ont_explorer.ontology_loader()

 # read in ontology data
 with open('resources/ontologies/master_ontology_dictionary.pickle', 'rb') as handle:
     ont_data = pickle.load(handle)
 handle.close()

 # process clinical data
 mapper = ConceptAnnotator(clinical_file='resources/clinical_data/omop2obo_conditions_june2020.csv',
                           ontology_dictionary={k: v for k, v in ont_data.items() if k in ['hp', 'mondo']},
                           merge=True,
                           primary_key='CONCEPT_ID',
                           concept_codes=tuple(['CONCEPT_SOURCE_CODE']),
                           concept_strings=tuple(['CONCEPT_LABEL', 'CONCEPT_SYNONYM']),
                           ancestor_codes=tuple(['ANCESTOR_SOURCE_CODE']),
                           ancestor_strings=tuple(['ANCESTOR_LABEL']),
                           umls_mrconso_file=glob.glob('resources/mappings/*MRCONSO*')[0] if len(glob.glob('resources/mappings/*MRCONSO*')) > 0 else None,
                           umls_mrsty_file=glob.glob('resources/mappings/*MRCONSO*')[0] if len(glob.glob('resources/mappings/*MRCONSO*')) > 0 else None)

    exact_mappings = mapper.clinical_concept_mapper()
    exact_mappings.to_csv(outfile + 'CONDITIONS' + date_today + '.csv', sep=',', index=False, header=True)
    # get column names -- used later to organize output
    start_cols = [i for i in exact_mappings.columns if not any(j for j in ['STR', 'DBXREF', 'EVIDENCE'] if j in i)]
    exact_cols = [i for i in exact_mappings.columns if i not in start_cols]

    # perform similarity mapping
    if tfidf_mapping is not None:
        sim = SimilarStringFinder(clinical_file=outfile + 'CONDITIONS' + date_today + '.csv',
                                  ontology_dictionary={k: v for k, v in ont_data.items() if k in ['hp', 'mondo']},
                                  primary_key='CONCEPT_ID',
                                  concept_strings=tuple(['CONCEPT_LABEL', 'CONCEPT_SYNONYM']))

        sim_mappings = sim.performs_similarity_search()
        sim_mappings = sim_mappings[['CONCEPT_ID'] + [x for x in sim_mappings.columns if 'SIM' in x]].drop_duplicates()
        # get column names -- used later to organize output
        sim_cols = [i for i in sim_mappings.columns if not any(j for j in start_cols if j in i)]

        # merge dbXref, exact string, and TF-IDF similarity results
        merged_scores = pd.merge(exact_mappings, sim_mappings, how='left', on='CONCEPT_ID')
        # re-order columns and write out data
        merged_scores = merged_scores[start_cols + exact_cols + sim_cols]
        merged_scores.to_csv(outfile + clinical_domain.upper() + date_today + '.csv', sep=',', index=False, header=True)

|

*COMMAND LINE* ➞ `main.py <https://github.com/callahantiff/OMOP2OBO/blob/master/main.py>`_

.. code:: bash

  python main.py --help
  Usage: main.py [OPTIONS]

  The OMOP2OBO package provides functionality to assist with mapping OMOP standard clinical terminology
  concepts to OBO terms. Successfully running this program requires several input parameters, which are
  specified below:


  PARAMETERS:
      ont_file: 'resources/oontology_source_list.txt'
      tfidf_mapping: "yes" if want to perform cosine similarity mapping using a TF-IDF matrix.
      clinical_domain: clinical domain of input data (i.e. "conditions", "drugs", or "measurements").
      merge: A bool specifying whether to merge UMLS SAB codes with OMOP source codes once or twice.
      onts: A comma-separated list of ontology prefixes that matches 'resources/oontology_source_list.txt'.
      clinical_data: The filepath to the clinical data needing mapping.
      primary_key: The name of the file to use as the primary key.
      concept_codes: A comma-separated list of concept-level codes to use for DbXRef mapping.
      concept_strings: A comma-separated list of concept-level strings to map to use for exact string mapping.
      ancestor_codes: A comma-separated list of ancestor-level codes to use for DbXRef mapping.
      ancestor_strings: A comma-separated list of ancestor-level strings to map to use for exact string mapping.
      outfile: The filepath for where to write output data to.

  Several dependencies must be addressed before running this file. Please see the README for instructions.

  Options:
    --ont_file PATH          [required]
    --tfidf_mapping TEXT     [required]
    --clinical_domain TEXT   [required]
    --merge                  [required]
    --ont TEXT               [required]
    --clinical_data PATH     [required]
    --primary_key TEXT       [required]
    --concept_codes TEXT     [required]
    --concept_strings TEXT
    --ancestor_codes TEXT
    --ancestor_strings TEXT
    --outfile TEXT           [required]
    --help                   Show this message and exit.

If you follow the instructions for how to format clinical data (`here <https://github.com/callahantiff/OMOP2OBO/tree/master/resources/clinical_data>`__) and/or if taking the data that results from running our queries `here <https://github.com/callahantiff/OMOP2OBO/tree/master/resources/clinical_data>`__), ``omop2obo`` can be run with the following call on the command line (with minor updates to the csv filename):

.. code:: bash

 python main.py --clinical_domain condition --onts hp --onts mondo --clinical_data resources/clinical_data/omop2obo_conditions_june2020.csv

|

*JUPYTER NOTEBOOK* ➞ `omop2obo_notebook.ipynb <https://github.com/callahantiff/OMOP2OBO/blob/master/omop2obo_notebook.ipynb>`_

|

Contributing
############

Please read `CONTRIBUTING.md <https://github.com/callahantiff/biolater/blob/master/CONTRIBUTING.md>`__ for details on our code of conduct, and the process for submitting pull requests to us.

|

License
#######

This project is licensed under MIT - see the `LICENSE.md <https://github.com/callahantiff/OMOP2OBO/blob/master/LICENSE>`__ file for details.

|

Citing this Work
################

.. code:: shell

   @software{callahan_tiffany_j_2020_3902767,
             author     =  {Callahan, Tiffany J},
             title      = {OMOP2OBO},
             month      = jun,
             year       = 2020,
             publisher  = {Zenodo},
             version    = {v1.0.0},
             doi        = {10.5281/zenodo.3902767},
             url        = {https://doi.org/10.5281/zenodo.3902767}.
      }

|

Contact
#######

We’d love to hear from you! To get in touch with us, please join or start a new `Discussion`_, `create an issue`_
or `send us an email`_ 💌

.. |logo| image:: https://user-images.githubusercontent.com/8030363/140855940-1aa2dcd5-a1b3-469a-97cf-a466d6e20b25.png
   :width: 1500

.. |dashboard1| image:: https://github.com/callahantiff/OMOP2OBO_Dashboard/blob/master/figures/summary.png
   :width: 500
   
.. |dashboard2| image:: https://github.com/callahantiff/OMOP2OBO_Dashboard/blob/master/figures/data.png
   :width: 500
   :height: 300

.. |github_action| image:: https://github.com/callahantiff/OMOP2OBO/workflows/Domo%20Arigato%20CI%20Roboto/badge.svg
   :target: https://github.com/callahantiff/OMOP2OBO/actions?query=workflow%3A%22Domo+Arigato+CI+Roboto%22
   :alt: GitHub Action CI-Workflow

.. |sonar_quality| image:: https://sonarcloud.io/api/project_badges/measure?project=callahantiff_OMOP2OBO&metric=alert_status
    :target: https://sonarcloud.io/dashboard/index/callahantiff_OMOP2OBO
    :alt: SonarCloud Quality

.. |sonar_maintainability| image:: https://sonarcloud.io/api/project_badges/measure?project=callahantiff_OMOP2OBO&metric=sqale_rating
    :target: https://sonarcloud.io/dashboard/index/callahantiff_OMOP2OBO
    :alt: SonarCloud Maintainability

.. |sonar_coverage| image:: https://sonarcloud.io/api/project_badges/measure?project=callahantiff_OMOP2OBO&metric=coverage
    :target: https://sonarcloud.io/dashboard/index/callahantiff_OMOP2OBO
    :alt: SonarCloud Coverage

.. |coveralls| image:: https://coveralls.io/repos/github/callahantiff/OMOP2OBO/badge.svg
    :target: https://coveralls.io/github/callahantiff/OMOP2OBO
    :alt: Coveralls Coverage

.. |pip| image:: https://badge.fury.io/py/omop2obo.svg
    :target: https://pypi.org/project/omop2obo/
    :alt: Pypi project

.. |downloads| image:: https://pepy.tech/badge/omop2obo
    :target: https://pepy.tech/badge/omop2obo
    :alt: Pypi total project downloads

.. |codacy| image:: https://app.codacy.com/project/badge/Grade/a6b93723ccb2466bb20cdb9763c2f0c5
    :target: https://www.codacy.com/manual/callahantiff/OMOP2OBO?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=callahantiff/OMOP2OBO&amp;utm_campaign=Badge_Grade
    :alt: Codacy Maintainability

.. |code_climate_maintainability| image:: https://api.codeclimate.com/v1/badges/5ad93b637f347255c848/maintainability
    :target: https://codeclimate.com/github/callahantiff/OMOP2OBO/maintainability
    :alt: Maintainability

.. |code_climate_coverage| image:: https://api.codeclimate.com/v1/badges/5ad93b637f347255c848/test_coverage
    :target: https://codeclimate.com/github/callahantiff/OMOP2OBO/test_coverage
    :alt: Code Climate Coverage
    
.. |ABRA| image:: https://img.shields.io/badge/ReproducibleResearch-AbraCollaboratory-magenta.svg
   :target: https://github.com/callahantiff/Abra-Collaboratory 
    
.. _OMOP: https://www.ohdsi.org/data-standardization/the-common-data-model/

.. _OBOs: http://www.obofoundry.org/

.. _Wiki: https://github.com/callahantiff/BioLater/wiki

.. _`create an issue`: https://github.com/callahantiff/OMOP2OBO/issues/new/choose

.. _`send us an email`: https://mail.google.com/mail/u/0/?view=cm&fs=1&tf=1&to=callahantiff@gmail.com

.. _`Discussion`: https://github.com/callahantiff/OMOP2OBO/discussions
