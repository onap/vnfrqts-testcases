.. Modifications Copyright © 2017-2018 AT&T Intellectual Property.

.. Licensed under the Creative Commons License, Attribution 4.0 Intl.
   (the "License"); you may not use this documentation except in compliance
   with the License. You may obtain a copy of the License at

.. https://creativecommons.org/licenses/by/4.0/

.. Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.


Appendix
========

.. _info-elements:

List of Requirements with associated Tests
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Currently, there VNFs can be packaged as HEAT templates or in a CSAR file
using TOSCA.  At this stage, there are two different tools used for
validating the packages based on the package type:

* CSAR/TOSCA packages leverage VNFSDK
* HEAT packages leverage VVP

HEAT Package Validations
------------------------

This table shows all the requirements within the VNF Requirements project and
if they are validated by VVP.  If they are validated by VVP, then
the test module and test method is provided.  This is generated
dynamically within the VVP project, where it pulls down the latest JSON from
:doc:`Req List </../../../../vnfrqts/requirements.git/docs/Chapter9/index>`
and maps the requirements to the tests in VVP to output this table.

**Note: Tests on the bottom do not map to any requirements.**

**Note: VVP only validates Heat for Requirements in Chapter 5.**

.. admonition:: Download

   You can download the table
   `here <https://nexus.onap.org/content/sites/raw/org.onap.vvp.validation-scripts/master/traceability.csv>`_.

.. csv-table:: **Test Traceability**
   :name: traceability-matrix
   :url: https://nexus.onap.org/content/sites/raw/org.onap.vvp.validation-scripts/master/rst.csv
   :header-rows: 1
   :align: center
   :widths: auto

.. _info-elements-range-limits:

CSAR/TOSCA Package Validations
------------------------------

Please refer to the VNFSDK project's `list of verified requirements <https://onap.readthedocs.io/en/latest/submodules/vnfsdk/model.git/docs/files/VNFSDK-LFN-CVC.html#casablanca-implemented-requriements>`__
for the current coverage for CSAR and TOSCA.


VNF Requirements corresponding Information Elements w/Range limits
------------------------------------------------------------------------------

Will be generated in future releases.
