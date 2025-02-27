# Copyright (c) Microsoft Corporation. All rights reserved.
# SPDX-License-Identifier: MIT

#cspell: words sgxenclave
cmake_minimum_required (VERSION 3.13)

project (attestation-attestation LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED True)

macro (define_sample samplename)
add_executable (
  attestation-${samplename}
  ${samplename}.cpp
  attestation_collateral.cpp 
  attestation_collateral.hpp)

CREATE_PER_SERVICE_TARGET_BUILD_FOR_SAMPLE(attestation attestation-${samplename})

target_link_libraries(attestation-${samplename} PRIVATE azure-security-attestation get-env-helper)

endmacro()


define_sample(attest_sgxenclave)
define_sample(attest_sgxenclave_with_runtime_json)
define_sample(attest_sgxenclave_with_runtime_binary)
define_sample(attest_openenclave_with_draft_policy)
define_sample(attest_openenclave_shared)

