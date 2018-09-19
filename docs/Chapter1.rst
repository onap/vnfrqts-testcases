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


**VNF Package Test Cases**
==========================

VNF Package Information Element Present
---------------------------------------

Summary
^^^^^^^

This test case validates whether information elements corresponding to
VNF requirements are present in the VNF Package

ONAP Actors (VNF, Operator, ONAP Platform components etc.)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. VNF Package
2. VNF Requirements
3. ONAP Information Model

Preconditions (ONAP, VNF states, test equipment/ data patterns, measurements)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. VNF Package available
2. VNF Requirements related to VNF Package identified (Mandatory or Optional)
3. Information Elements corresponding to these VNF Package requirements
   identified

Operational sequence (e.g. Message Sequence chart + text explanations)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Search the VNF Package for the Presence/ Absence of each
   Information Elementidentified in the VNF Package requirements.
2. Flag as an error any Mandatory information Elements that are missing
3. Report and optional Information Elements that are present.

Post conditions (any post processing of the measurements, any cleanup of the ONAP configuration, reset of the test equipment etc.)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Generate consolidated report on presence/Absence of Information Elements
   identified in VNF Requirements

Test Result decision ( measurement  decision criteria )
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Fail if and Mandatory Information Elements are Absent.


VNF Package Information Element within Range Limits
---------------------------------------------------

Summary
^^^^^^^

This test case validates whether information elements corresponding
to VNF requirements are present in the VNF Package

ONAP Actors (VNF, Operator, ONAP Platform components etc.)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. VNF Package
2. VNF Requirements
3. ONAP Information Model

Preconditions (ONAP, VNF states, test equipment/ data patterns, measurements)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. VNF Package available
2. VNF Requirements related to VNF Package identified (Mandatory or Optional)
3. Information Elements corresponding to these VNF Package requirements
   identified
4. Range Limits for Information Elements identified

Operational sequence (e.g. Message Sequence chart + text explanations)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Search the VNF Package for the Presence/ Absence of each Information
   Element identified in the VNF Package requirements.
2. Flag as an error any Mandatory information Elements that are missing

Post conditions (any post processing of the measurements, any cleanup of the ONAP configuration, reset of the test equipment etc.)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Generate consolidated report on presence/Absence of Information Elements
   identified in VNF Requirements

Test Result decision ( measurement  decision criteria )
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Fail if and Mandatory Information Elements are Absent.


