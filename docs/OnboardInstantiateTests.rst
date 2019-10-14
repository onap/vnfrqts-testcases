.. Modifications Copyright © 2019 AT&T Intellectual Property.

.. Licensed under the Creative Commons License, Attribution 4.0 Intl.
   (the "License"); you may not use this documentation except in compliance
   with the License. You may obtain a copy of the License at

.. https://creativecommons.org/licenses/by/4.0/

.. Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.


VNF Onboard and Instantiate Test Specification
==============================================

.. contents::
   :local:

Scope
-----

This specification defines the logical steps and activities required
to implement a test case that validates that a arbitrary
Virtual Network Function (VNF) that is packaged in compliance with the
ONAP VNF Requirements can be successfully be onboarded into
ONAP and instantiated. This specification only covers up to
instantiation of the VNF and does not address the VNF's compliance with
requirements governing other lifecycle functions controlled by
ONAP (ex: Lifecycle Management, Monitoring, etc.)

Two test cases will be defined based on the VNF package used:

1. ZIP file containing ONAP-compliant OpenStack Heat
2. Cloud Service Archive (CSAR) containing a Topology and Orchestration
   Specification for Cloud Applications (TOSCA) VNF Descriptor

.. _vnfrqts_tc_instantiate_references:

References
----------
* :doc:`ONAP VNF Requirements </../../../vnfrqts/requirements.git/docs/index>`
* :doc:`Setting up ONAP </../../../../../guides/onap-developer/settingup/index>`
* `OPNFV Verification Program for VNFs <https://vnf-verified.lfnetworking.org/#/>`__

Actors
------

The following defines the various actors that will be referenced within this
specification.  It is expected and permissable that a given user or entity
can serve in multiple roles for the purposes of the test.

* **VNF Provider** - Responsible for developing, packaging, and distributing a
  VNF that is compliant with ONAP VNF Requirements as well as providing any
  additional artifacts required to setup the **Test Lab** or **Test Engine**.
* **Test Lab** - Hosts the ONAP and Cloud environment used to execute the test
  cases. The environment will host a deployed instance of ONAP using the
  official El Alto release of ONAP and a compatible OpenStack cloud instance.
* **Test Lab Provider** - Responsible for establishing the **Test Lab** and
  supporting the **Tester** in the configuration of the **Test Lab** for any
  VNF specific requirements such as virtual machine images or networks.  This
  will include providing the **Test Engine** access to the necessary
  ONAP APIs/GUIs as well as access to the OpenStack APIs.
* **Tester** - Responsible for:

   1. Ensuring the test lab is configured per the VNF's requirements and needs.
   2. Configuring the **Test Engine** for execution.  The artifacts required
      will be provided by the **VNF Provider**.
   3. Executing the the test cases using the **Test Engine**.
   4. Reporting the results of the test case to the **VNF Provider**.

* **Test Engine** - Provides automation of the test execution and verification
  of the success or failure of the individual test cases.  The **Test Engine**
  must also provide further documentation on how it and the **Test Lab**
  must be configured for successful execution and verification of the test
  cases.


Test Case Description: VNF Onboarding and Instantiation using OpenStack Heat
----------------------------------------------------------------------------

This test case is specific to executing and validating the onboarding of a VNF
using OpenStack Heat.

Assumptions
^^^^^^^^^^^

* The specific configuration of the Vendor License Model is not relevant to the
  successful execution of this test case.  The **Test Engine** shall create a
  generic Vendor License Model to assign to the VNF for the purposes of this
  test.
* Testing will support the instantiation of a SDC Service that is composed
  of a single VNF.  The scope of this test is focused on the instantiation
  of a single VNF defined in a single Heat package.  Testing services that
  comprise multiple VNFs is beyond the scope of this specification.
* The **Test Engine** will have access to the ONAP APIs in terms of both
  network connectivity and API access.
* VNF Instantiation for either ONAP legacy VNF API or Generic Resource API is
  supported.


Prerequisites
^^^^^^^^^^^^^

* **VNF Provider** has:

   * Provided the **Tester** the VNF package containing OpenStack Heat that has
     been certified compliant by the OPNFV Verification Program for
     VNFs or validated by the El Alto release of the
     :doc:`ONAP VNF Validation Platform </../../../../vvp/documentation.git/docs/index>`
   * Provided the **Tester** any custom virtual machine image required by the
     VNF
   * Provided the **Tester** network requirements for any ONAP external networks
     (i.e. networks not created in the Heat template itself) required by the
     VNF.
   * Provided the **Tester** with any additional artifacts required by the
     **Test Engine**. Additional artifacts required by the **Test Engine** are
     outside the scope of this document.  Please refer to the **Test Engine**
     documentation for more details.

* **Test Lab Provider** has:

    * Successfully deployed an OpenStack cloud instance for ONAP to deploy and
      instantiate the VNF.
    * Successfully deployed the certified El Alto release version of ONAP.
    * Configured the ONAP instance to work with the OpenStack instance.

       * **NOTE:** Documentation of OpenStack and ONAP setup are beyond the
         scope of this document. Please refer to the
         :ref:`vnfrqts_tc_instantiate_references` section for more information.

    * Provided the **Test Engine** network connectivity to both the ONAP and
      OpenStack control planes.
    * Provided the **Test Engine** permissions to invoke the required ONAP and
      OpenStack APIs.  Full details to be provided in the **Test Engine**
      documentation.

* The **Tester** has:

    * Created any external networks in ONAP and OpenStack cloud environment in
      compliance with the **VNF Providers** request and specification.
    * Registered any custom virtual machine images provided by the
      **VNF Provider** in the OpenStack Glance repository.
    * Configured the **Test Engine** with the necessary artifacts from the
      **VNF Provider** for successful test execution.  The **Test Engine**
      must provide the full documentation on what is required to configure
      it for successful execution.
    * Ensured connectivity from the **Test Engine** to any Operations,
      Administration, and Management (OAM) interfaces provided by the VNF.
      This connectivity must allow PING requests which will be used as part
      of the validation process to ensure the VNF has been properly
      instantiated.


Execution Steps
^^^^^^^^^^^^^^^

The following steps will all be executed by the **Test Engine**.  The steps
depicts the actions that will be taken and which ONAP component the
**Test Engine** will interact with to perform the action.

Failure encountered at any step will halt all subsequent steps and result in
the overall failure of the test case.

Any additional required fields that must be assigned or input within ONAP will
be defined in a configuration file whose format will be defined in the
documentation of the **Test Engine**.

**Steps**

1. Execute VVP validation scripts to ensure VNF Heat Templates are compliant
   with the VNF Heat Template Requirements.

2. Create the generic Vendor License Model (VLM) in SDC

3. Create the Vendor Software Product (VSP) in SDC.  The VSP will be
   auto-assigned a unique name to avoid collisions with other VSPs in the
   lab environment.

4. Upload the ONAP-compliant Heat archive (zip file) as an artifact of the VSP in SDC.

5. Assign any "Unassigned Files" in SDC to Artifacts

6. Validate the VSP and ensure no SDC **errors** are raised, but **warnings**
   are acceptable.  If errors are reported, then halt the test and report a
   failure.

7. Assign the generic VLM to the VSP in SDC.

8. Create the Virtual Function (VF) in SD.  The VF will be
   auto-assigned a unique name to avoid collisions with other VSPs in the
   lab environment.

9. Create the Service in SDC. The Service will be
   auto-assigned a unique name to avoid collisions with other VSPs in the
   lab environment.

10. Assign the VF/VNF to the Service Model in SDC.

11. Distribute the Service Model from SDC.

12. Register Preload (i.e. per instance configuration data) with SDNC

13. For each VF module in the VNF, starting with the base module, trigger
    instantiation from VID.

14. After VNF Instantiation, query openstack for heat stack details to 
    validate successful instantiation.

**Pass/Fail Criteria**

Following, or during, test execution the tests below will be executed to
evaluate the success of the overall test case.  As previously stated above, if
any individual test step fails, then the test case will fail.

1. The Heat stack has been successfully created in OpenStack without errors

2. The Heat stack configuration matches the definition from the associated
   Heat templates and environment settings provided as input (or derived by)
   the **Test Engine**


Test Case Description: VNF Onboarding and Instantiation using TOSCA
-------------------------------------------------------------------

This test case is specific to executing and validating the onboarding of a VNF
written in TOSCA and packaged in a CSAR.

Assumptions
^^^^^^^^^^^

* The specific configuration of the Vendor License Model is not relevant to the
  successful execution of this test case.  The **Test Engine** shall create a
  generic Vendor License Model to assign to the VNF for the purposes of this
  test.
* Testing will support the instantiation of a SDC Service that is composed
  of a single VNF.  The scope of this test is focused on the instantiation
  of a single VNF defined in a single TOSCA package.  Testing services that
  comprise multiple VNFs is beyond the scope of this specification.
* The **Test Engine** will have access to the ONAP APIs in terms of both
  network connectivity and API access.
* All instantiations will use the ONAP Generic Resource API from VFC instead
  of the legacy VNF API.


Prerequisites
^^^^^^^^^^^^^

* **VNF Provider** has:

   * Provided the **Tester** the TOSCA based VNF Package that has
     been certified compliant by the LFN OVP(OPNFV Verification Program) for
     VNFs or validated by the El Alto release of the ONAP VNFSDK
   * Provided the **Tester** any custom virtual machine image required by the
     VNF
   * Provided the **Tester** network requirements for any ONAP external networks
     (i.e. networks not created in the TOSCA template itself) required by the
     VNF.
   * Provided the **Tester** with any additional artifacts required by the
     **Test Engine**. Additional artifacts required by the **Test Engine** are
     outside the scope of this document.  Please refer to the **Test Engine**
     documentation for more details.

* **Test Lab Provider** has:

    * Successfully deployed an OpenStack cloud instance for ONAP to deploy and
      instantiate the VNF.
    * Successfully deployed the certified El Alto release version of ONAP.
    * Configured the ONAP instance to work with the OpenStack instance.

       * **NOTE:** Documentation of OpenStack and ONAP setup are beyond the
         scope of this document. Please refer to the
         :ref:`vnfrqts_tc_instantiate_references` section for more information.

    * Provided the **Test Engine** network connectivity to both the ONAP and
      OpenStack control planes.
    * Provided the **Test Engine** permissions to invoke the required ONAP and
      OpenStack APIs.  Full details to be provided in the **Test Engine**
      documentation.

* The **Tester** has:

    * Created any external networks in ONAP and OpenStack cloud environment in
      compliance with the **VNF Providers** request and specification.
    * Registered any custom virtual machine images provided by the
      **VNF Provider** in the OpenStack Glance repository.
    * Configured the **Test Engine** with the necessary artifacts from the
      **VNF Provider** for successful test execution.  The **Test Engine**
      must provide the full documentation on what is required to configure
      it for successful execution.
    * Ensured connectivity from the **Test Engine** to any Operations,
      Administration, and Management (OAM) interfaces provided by the VNF.
      This connectivity must allow PING requests which will be used as part
      of the validation process to ensure the VNF has been properly
      instantiated.


Execution Steps
^^^^^^^^^^^^^^^

The following steps will all be executed by the **Test Engine**.  The steps
depicts the actions that will be taken and which ONAP component the
**Test Engine** will interact with to perform the action.

Failure encountered at any step will halt all subsequent steps and result in
the overall failure of the test case.

Any additional required fields that must be assigned or input within ONAP will
be defined in a configuration file whose format will be defined in the
documentation of the **Test Engine**.

**Steps**

1. Register VIM and VNFM to ONAP environment through ESR.

2. Create the generic Vendor License Model (VLM) in SDC.

3. Create the Vendor Software Product (VSP) in SDC.  The VSP will be
   auto-assigned a unique name to avoid collisions with other VSPs in the
   lab environment.

4. Upload the ONAP-compliant TOSCA archive (zip file) as an artifact of the VSP in SDC.

5. Assign any "Unassigned Files" in SDC to Artifacts.

6. Validate the VSP and ensure no SDC **errors** are raised, but **warnings**
   are acceptable.  If errors are reported, then halt the test and report a
   failure.

7. Assign the generic VLM to the VSP in SDC.

8. Create the Virtual Function (VF) in SDC. The VF will be
   auto-assigned a unique name to avoid collisions with other VSPs in the
   lab environment.

9. Add original VNF CSAR as artifacts to VF.

10.	Assign nf_type property with required VNFM driver.

11.	Certify VF model

12. Create the Service in SDC. The Service will be
   auto-assigned a unique name to avoid collisions with other VSPs in the
   lab environment.

13. Assign the VF/VNF to the Service Model in SDC.

14.	Attach original NS CSAR with service model.

15.	Test the Service model in SDC.

16.	Approve the Service model in SDC.

17. Distribute the Service Model from SDC.

18.	Onboard VNF CSAR from SDC to VFC Catalog.

19.	Onboard Service CSAR from SDC to VFC Catalog.

20.	Call VFC NSLCM Create API to create service instance.

21.	Call VFC NSLCM Instantiate API to instantiate service.

**Pass/Fail Criteria**

Following, or during, test execution the tests below will be executed to
evaluate the success of the overall test case.  As previously stated above, if
any individual test step fails, then the test case will fail.

1. The virtual machine has been successfully created in OpenStack without errors.

2. Each virtual machine in the OpenStack must have a corresponding
   ``vserver`` ONAP's Available and Active Inventory (AAI) component with all
   required data elements.

3. The VNF has a ``Generic-VNF`` object recorded in AAI with all required data elements.

