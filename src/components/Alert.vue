<template>
  <v-card
    class="mx-auto"
    outlined
  >
    <v-list-item>
      <v-container>
				<v-row>
					<v-col 
					cols="12"
					sm="6"
					md="4"
					class="d-flex">
						<v-subheader>Card ID</v-subheader>
						<v-text-field
							v-model="info.CarID"
						></v-text-field>
					</v-col>
					<v-col 
						cols="12"
						sm="6"
						md="4"
						class="d-flex">
						<v-subheader>Prod ID</v-subheader>
						<v-select
							:items="info.ProdID"
						></v-select>
					</v-col>
					<v-col
						cols="12"
						sm="6"
						md="4"
						class="d-flex justify-center align-center">
						<v-subheader>Test Name</v-subheader>
						<v-text-field
							v-model="info.TestName"
						></v-text-field>
						<v-btn
							depressed
							color="primary"
						>
							Query
						</v-btn>
					</v-col>
				</v-row>
				<v-row>
					<v-tabs>
						<v-tab
							v-for="item in tab"
							:key="item">
							{{ item }}
						</v-tab>
						<v-tab-item>
							<v-card>
								<v-row>
									<v-col
										cols="12"
										md="6"
										class="d-flex">
										<v-subheader>{{ base[0].data[0].key }}</v-subheader>
										<v-text-field
											v-model="base[0].data[0].value"
										></v-text-field>
									</v-col>
									<v-col
										cols="12"
										md="6"
										class="d-flex justify-center align-center">
										<v-subheader>{{ base[0].data[3].key }}</v-subheader>
										<v-text-field
											v-model="base[0].data[3].value"
										></v-text-field>
										<v-dialog
											v-model="dialog"
											width="500"
										>
											<template v-slot:activator="{ on, attrs }">
												<v-btn
													depressed
													color="info"
													dark
													v-bind="attrs"
													v-on="on"
												>
													{{ base[0].data[3].btn }}
												</v-btn>
											</template>

											<v-card>
												<v-card-title class="text-h4 grey lighten-2">
													Message Dialog
												</v-card-title>

												<v-card-text class="text-h5">
													Status is Prepare
												</v-card-text>

												<v-divider></v-divider>

												<v-card-actions>
													<v-spacer></v-spacer>
													<v-btn
														color="info"
														text
														@click="dialog = false"
													>
														OK
													</v-btn>
												</v-card-actions>
											</v-card>
										</v-dialog>
									</v-col>
									<v-col
										cols="12"
										md="6"
										class="d-flex">
										<v-subheader>{{ base[0].data[1].key }}</v-subheader>
										<v-text-field
											v-model="base[0].data[1].value"
										></v-text-field>
									</v-col>
									<v-col
										cols="12"
										md="6"
										class="d-flex">
										<v-subheader>{{ base[0].data[5].key }}</v-subheader>
										<v-text-field
											v-model="base[0].data[5].value"
										></v-text-field>
									</v-col>
									<v-col
										cols="12"
										md="6"
										class="d-flex">
										<v-subheader>{{ base[0].data[2].key }}</v-subheader>
										<v-text-field
											v-model="base[0].data[2].value"
										></v-text-field>
									</v-col>
									<v-col
										cols="12"
										md="6"
										class="d-flex justify-center align-center">
										<v-subheader>{{ base[0].data[9].key }}</v-subheader>
										<v-text-field
											v-model="base[0].data[9].value"
										></v-text-field>
										<v-subheader>{{ base[0].data[10].key }}</v-subheader>
										<v-text-field
											v-model="base[0].data[10].value"
										></v-text-field>
										<v-btn
											depressed
											:disabled="true"
											color="info"
										>
											{{ base[0].data[3].btn }}
										</v-btn>
									</v-col>
								</v-row>
							</v-card>
						</v-tab-item>
						<v-tab-item>
						<v-card>
							<v-row>
								<v-col
									cols="12"
									md="6">
									<v-col
										class="d-flex">
										<v-subheader>{{ detail[0].data[0].key }}</v-subheader>
										<v-text-field
											v-model="detail[0].data[0].value"
										></v-text-field>
									</v-col>
									<v-col
										class="d-flex">
										<v-subheader>{{ detail[0].data[1].key }}</v-subheader>
										<v-text-field
											v-model="detail[0].data[1].value"
										></v-text-field>
									</v-col>
									<v-col
										class="d-flex">
										<v-subheader>{{ detail[0].data[2].key }}</v-subheader>
										<v-text-field
											v-model="detail[0].data[2].value"
										></v-text-field>
									</v-col>
									<v-col
										class="d-flex">
										<v-subheader>{{ detail[0].data[4].key }}</v-subheader>
										<v-text-field
											v-model="detail[0].data[4].value"
										></v-text-field>
									</v-col>
								</v-col>
								<v-col
									cols="12"
									md="6">
									<v-col
										class="d-flex">
										<v-subheader>{{ detail[0].data[3].key }}</v-subheader>
										<v-text-field
											v-model="detail[0].data[3].value"
										></v-text-field>
									</v-col>
									<v-card>
										<v-data-table
											:headers="headers"
											:items="detail[0].data[5].value" hide-default-footer>
										</v-data-table>
									</v-card>
								</v-col>
							</v-row>
						</v-card>
						</v-tab-item>
					</v-tabs>
				</v-row>
			</v-container>
    </v-list-item>
  </v-card>
</template>

<script>
export default {
	data: () => ({
		dialog: false,
		tab: [
			'Base Information',
			'Detail',
		],
		info: {
			CarID: 'CAR111222',
			ProdID: ['ProdAABB.11','ProdAABB.22'],
			TestName: 'ProdTestName'
		},
		base: [{
			data: [
				{key: 'Type', value: 'Production'},
				{key: 'Sub Type', value: 'Production'},
				{key: 'Last Claimed TS', value: '2021-10-13-01.27.00.498213'},
				{key: 'Lot Status', value: 'Waiting', btn: 'Info'},
				{key: 'Flow Batch ID', value: ''},
				{key: 'Description', value: 'This is Production Desc'},
				{key: 'Lot Owner ID', value: 'MFG', btn: 'Gate Pass >>'},
				{key: 'Lot Cost Owner ID', value: 'MFG', btn: 'Inter Bay Xfer'},
				{key: 'Lot Owner Dept', value: 'MFG', btn: 'Stock Out'},
				{key: 'Count', value: '1'},
				{key: 'Color', value: 'Red'},
			]}
		],
		detail: [{
			data: [
				{key: 'Type', value: 'Production'},
				{key: 'Sub Type', value: 'Production'},
				{key: 'Due TS', value: '2020-07-04-11.43.00.000213'},
				{key: 'Current Status', value: 'Waiting'},
				{key: 'Bank ID', value: ''},
				{key: 'Status List', value: [
					{StateName:'Previous State', StateValue:'ACTIVE'},
					{StateName:'Test State', StateValue:'Always OK'}]},
		]}],
  }),
	computed: {
		headers () {
			let headerList = [];
			const objectKey = Object.keys(this.detail[0].data[5].value[0]);
			objectKey.forEach(item => {
				headerList.push({
					text: item,
					align: 'ceenter',
					value: item
				})
			})
			return headerList;
		}
	}
}
</script>
