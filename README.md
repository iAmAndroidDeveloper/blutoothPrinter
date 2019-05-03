# blutoothPrinter
 if (SharedPreferencesMain.getDefaults("manager_deviceId", context) != null) {
                BluetoothAdapter btAdapter = BluetoothAdapter.getDefaultAdapter();
                Set<BluetoothDevice> mPairedDevices = btAdapter.getBondedDevices();
                if (mPairedDevices.size() > 0) {
                    for (BluetoothDevice mDevice : mPairedDevices) {

                        if (SharedPreferencesMain.getDefaults("manager_deviceId", context).equalsIgnoreCase(mDevice.getAddress())) {

                            final BluetoothPrinter mPrinter = new BluetoothPrinter(mDevice);
                            mPrinter.connectPrinter(new BluetoothPrinter.PrinterConnectListener() {
                                @Override
                                public void onConnected() {
                                    mPrinter.printMonthlyKOT(list);
                                    mPrinter.finish();
                                }

                                @Override
                                public void onFailed() {
                                    Log.d("BluetoothPrinter", "Conection failed");

                                }
                            });
                            break;
                        }

                    }
                }

            } else {
                Toast.makeText(context, "First connect manager printer", Toast.LENGTH_SHORT).show();
            }
