<script lang="ts">
    import { BluetoothConnected, BluetoothIcon } from "lucide-svelte";
    import { onMount } from "svelte";

    const requestBluetoothDevices = () => {
        ((navigator as any).bluetooth as any)
            .requestDevice({
                acceptAllDevices: true,
                optionalServices: ["battery_service"], // Required to access service later.
            })
            .then((device: any) => {
                console.log({ device });
                device.gatt.connect();
            })
            .catch((error: any) => {
                console.error(error);
            });
    };

    onMount(() => {});
</script>

<div class=" container mt-8 overflow-x-auto">
    <table class="table">
        <!-- head -->
        <thead>
            <tr>
                <th>
                    <label>
                        <input type="checkbox" class="checkbox" />
                    </label>
                </th>
                <th>Name</th>
                <th>Status</th>
                <th>Last Connected</th>
                <th></th>
            </tr>
        </thead>
        <tbody>
            <!-- row 1 -->
            <tr>
                <th>
                    <label>
                        <input type="checkbox" class="checkbox" />
                    </label>
                </th>
                <td>
                    <div class="flex justify-items-center items-center gap-3">
                        <div class="avatar flex items-center justify-center">
                            <BluetoothIcon />
                        </div>
                        <div>
                            <div class="font-bold">Hart Hagerty</div>
                            <div class="text-sm opacity-50">United States</div>
                        </div>
                    </div>
                </td>
                <td>
                    Zemlak, Daniel and Leannon
                    <br />
                    <span class="badge badge-ghost badge-sm"
                        >Desktop Support Technician</span
                    >
                </td>
                <td>Monday</td>
                <th>
                    <button
                        on:click={requestBluetoothDevices}
                        class="btn btn-success btn-xs"
                        ><BluetoothConnected size={12} /> Connect</button
                    >
                </th>
            </tr>
        </tbody>
    </table>
</div>
