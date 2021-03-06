# Copyright CERN and copyright holders of ALICE O2. This software is distributed
# under the terms of the GNU General Public License v3 (GPL Version 3), copied
# verbatim in the file "COPYING".
#
# See http://alice-o2.web.cern.ch/license for full licensing information.
#
# In applying this license CERN does not waive the privileges and immunities
# granted to it by virtue of its status as an Intergovernmental Organization or
# submit itself to any jurisdiction.

o2_add_library(TOFCalibration
               SOURCES src/CalibTOFapi.cxx
	               src/CalibTOF.cxx
		       src/CollectCalibInfoTOF.cxx
                       src/LHCClockCalibrator.cxx
               PUBLIC_LINK_LIBRARIES O2::DataFormatsTOF O2::TOFBase
                                     O2::CCDB
	                             O2::DetectorsCalibration
				     ROOT::Minuit
	                             ms_gsl::ms_gsl)
				  
				   
o2_target_root_dictionary(TOFCalibration
                          HEADERS include/TOFCalibration/CalibTOFapi.h
                                  include/TOFCalibration/CalibTOF.h
                                  include/TOFCalibration/LHCClockCalibrator.h
                                  include/TOFCalibration/CollectCalibInfoTOF.h)


o2_add_executable(data-generator-workflow
                  COMPONENT_NAME calibration
                  SOURCES testWorkflow/data-generator-workflow.cxx
                  PUBLIC_LINK_LIBRARIES O2::Framework
	                                O2::DataFormatsTOF
					O2::TOFBase)

o2_add_executable(lhc-clockphase-workflow
                  COMPONENT_NAME calibration
                  SOURCES testWorkflow/lhc-clockphase-workflow.cxx
                  PUBLIC_LINK_LIBRARIES O2::Framework
 		                        O2::TOFCalibration
	                                O2::DetectorsCalibration)

