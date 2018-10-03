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


**Appendix**
============

.. _info-elements:

List of VNF Requirements and corresponding Information Elements
--------------------------------------------------------------------------

You can download the table
:download:`here<ReqTable.csv>`

Included here is a table of VNF Requirements that are mainly referring to 
the testability of VNF Package requirements. It includes TOSCA or CSAR
artifact information as well as how it is testable (VNFSDK/VVP/SDC).
These requirements are mainly from :doc:`Chapter 5 <../../../../vnfrqts/requirements.git/docs/Chapter5/index>`
and the table has been generated manually to show users what specific
artifact is being tested by a specific requirement to make mapping possible
and to show coverage.

.. csv-table:: **Test Descriptions**
   :file: ReqTable.csv
   :header-rows: 1
   :align: center
   :widths: auto


List of Requirements with associated Tests
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can download the table
:download:`here<traceability.csv>`

This table shows all the requirements within the VNF Requirements project with
the section they are in, associated test names and modules. This is generated
dynamically within the VVP project, where it pulls down the latest JSON from
:doc:`Chapter 9 - Requirement List <../../../../vnfrqts/requirements.git/docs/Chapter9/index>`
and maps the requirements to the tests in VVP to output this table.

   **Note: Tests on the bottom do not map to any requirements.**

   **Note: VVP only validates Heat for Requirements in Chapter 5.**

.. csv-table:: **Test Traceability**
   :file: traceability.csv
   :header-rows: 1
   :align: center
   :widths: auto

.. _info-elements-range-limits:

VNF Requirements corresponding Information Elements w/Range limits
------------------------------------------------------------------------------

Will be generated in future releases.

.. [#4.1.1]
   Refer to NCSP’s Network Cloud specification

.. [#4.5.1]
   Refer to NCSP’s Network Cloud specification

.. [#4.5.2]
   Not currently supported in ONAP release 1

.. [#7.3.1]
   https://github.com/mbj4668/pyang

.. [#7.3.2]
   Recall that the Node Object **is required** to be identical across
   all VMs of a VNF invoked as part of the action except for the "name".

.. [#7.3.3]
   Upstream elements must provide the appropriate FQDN in the request to
   ONAP for the desired action.

.. [#7.3.4]
   Multiple ONAP actions may map to one playbook.

.. [#7.4.1]
   This option is not currently supported in ONAP and it is currently
   under consideration.

