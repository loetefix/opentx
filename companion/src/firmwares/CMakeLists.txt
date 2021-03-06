
set(firmwares_SRCS
  adjustmentreference.cpp
  boards.cpp
  curvedata.cpp
  curvereference.cpp
  customfunctiondata.cpp
  eeprominterface.cpp
  generalsettings.cpp
  gvardata.cpp
  input_data.cpp
  flightmodedata.cpp
  heli_data.cpp
  logicalswitchdata.cpp
  mixdata.cpp
  modeldata.cpp
  moduledata.cpp
  multiprotocols.cpp
  output_data.cpp
  radiodata.cpp
  radiodataconversionstate.cpp
  rawsource.cpp
  rawswitch.cpp
  sensordata.cpp
  telem_data.cpp
  afhds3.cpp
  ersky9x/ersky9xeeprom.cpp
  ersky9x/ersky9xinterface.cpp
  opentx/opentxeeprom.cpp
  opentx/opentxinterface.cpp
  )

string(REPLACE ".cpp" ".h" firmwares_HDRS "${firmwares_SRCS}")

list(APPEND firmwares_HDRS
  eepromimportexport.h
  moduledata.h
  helpersdata.h
  )

set(firmwares_QT
  curvereference.h
  )

qt5_wrap_cpp(firmwares_SRCS ${firmwares_QT})

add_library(firmwares ${firmwares_SRCS} ${firmwares_HDRS})
target_link_libraries(firmwares ${CPN_COMMON_LIB} datamodels Qt5::Core Qt5::Xml Qt5::Widgets)
target_include_directories(firmwares
  PRIVATE
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_CURRENT_BINARY_DIR}
  PUBLIC
    "${CMAKE_CURRENT_LIST_DIR}"
    "${CMAKE_CURRENT_LIST_DIR}/er9x"
    "${CMAKE_CURRENT_LIST_DIR}/ersky9x"
    "${CMAKE_CURRENT_LIST_DIR}/opentx"
  )
