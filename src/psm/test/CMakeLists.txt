include("openroad")

set(TEST_NAMES
    aes_test_vdd
    aes_test_vdd_set_node_density
    aes_test_vdd_set_node_density_fact
    aes_test_vss
    gcd_test_vdd
    gcd_no_vsrc
    gcd_write_sp_test_vdd
    gcd_em_test_vdd
    gcd_all_vss
    gcd_vss_no_vsrc
    gcd_sky130_vdd
    aes_asap7_vdd
    check_power_grid
    check_power_grid_disconnected
    check_power_grid_ok_disconnected
    check_power_grid_macros
    check_power_grid_disconnected_macro
    corners
    aes_test_bterms
    aes_test_multiple_bterms
    zerosoc_pads
    zerosoc_pads_check_only
    zerosoc_pads_check_only_disconnected
    pad_connected_by_abutment
)

foreach(TEST_NAME IN LISTS TEST_NAMES)
    or_integration_test("psm" ${TEST_NAME}  ${CMAKE_CURRENT_SOURCE_DIR}/regression)
endforeach()
