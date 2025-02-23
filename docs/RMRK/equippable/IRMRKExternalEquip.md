# IRMRKExternalEquip

*RMRK team*

> IRMRKExternalEquip

Interface smart contract of the RMRK external equippable module.



## Methods

### acceptAsset

```solidity
function acceptAsset(uint256 tokenId, uint256 index, uint64 assetId) external nonpayable
```

Accepts an asset at from the pending array of given token.

*Migrates the asset from the token&#39;s pending asset array to the token&#39;s active asset array.Active assets cannot be removed by anyone, but can be replaced by a new asset.Requirements:  - The caller must own the token or be approved to manage the token&#39;s assets  - `tokenId` must exist.  - `index` must be in range of the length of the pending asset array.Emits an {AssetAccepted} event.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId | uint256 | ID of the token for which to accept the pending asset |
| index | uint256 | Index of the asset in the pending array to accept |
| assetId | uint64 | ID of the asset expected to be in the index |

### approveForAssets

```solidity
function approveForAssets(address to, uint256 tokenId) external nonpayable
```

Used to grant permission to the user to manage token&#39;s assets.

*This differs from transfer approvals, as approvals are not cleared when the approved party accepts or  rejects an asset, or sets asset priorities. This approval is cleared on token transfer.Only a single account can be approved at a time, so approving the `0x0` address clears previous approvals.Requirements:  - The caller must own the token or be an approved operator.  - `tokenId` must exist.Emits an {ApprovalForAssets} event.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| to | address | Address of the account to grant the approval to |
| tokenId | uint256 | ID of the token for which the approval to manage the assets is granted |

### canTokenBeEquippedWithAssetIntoSlot

```solidity
function canTokenBeEquippedWithAssetIntoSlot(address parent, uint256 tokenId, uint64 assetId, uint64 slotId) external view returns (bool)
```

Used to verify whether a token can be equipped into a given parent&#39;s slot.



#### Parameters

| Name | Type | Description |
|---|---|---|
| parent | address | Address of the parent token&#39;s smart contract |
| tokenId | uint256 | ID of the token we want to equip |
| assetId | uint64 | ID of the asset associated with the token we want to equip |
| slotId | uint64 | ID of the slot that we want to equip the token into |

#### Returns

| Name | Type | Description |
|---|---|---|
| _0 | bool | A boolean indicating whether the token with the given asset can be equipped into the desired slot |

### equip

```solidity
function equip(IERC6220.IntakeEquip data) external nonpayable
```





#### Parameters

| Name | Type | Description |
|---|---|---|
| data | IERC6220.IntakeEquip | undefined |

### getActiveAssetPriorities

```solidity
function getActiveAssetPriorities(uint256 tokenId) external view returns (uint64[])
```

Used to retrieve the priorities of the active resoources of a given token.

*Asset priorities are a non-sequential array of uint64 values with an array size equal to active asset  priorites.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId | uint256 | ID of the token for which to retrieve the priorities of the active assets |

#### Returns

| Name | Type | Description |
|---|---|---|
| _0 | uint64[] | An array of priorities of the active assets of the given token |

### getActiveAssets

```solidity
function getActiveAssets(uint256 tokenId) external view returns (uint64[])
```

Used to retrieve IDs of the active assets of given token.

*Asset data is stored by reference, in order to access the data corresponding to the ID, call  `getAssetMetadata(tokenId, assetId)`.You can safely get 10k*

#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId | uint256 | ID of the token to retrieve the IDs of the active assets |

#### Returns

| Name | Type | Description |
|---|---|---|
| _0 | uint64[] | An array of active asset IDs of the given token |

### getApprovedForAssets

```solidity
function getApprovedForAssets(uint256 tokenId) external view returns (address)
```

Used to retrieve the address of the account approved to manage assets of a given token.

*Requirements:  - `tokenId` must exist.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId | uint256 | ID of the token for which to retrieve the approved address |

#### Returns

| Name | Type | Description |
|---|---|---|
| _0 | address | Address of the account that is approved to manage the specified token&#39;s assets |

### getAssetAndEquippableData

```solidity
function getAssetAndEquippableData(uint256 tokenId, uint64 assetId) external view returns (string metadataURI, uint64 equippableGroupId, address catalogAddress, uint64[] partIds)
```

Used to get the asset and equippable data associated with given `assetId`.



#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId | uint256 | ID of the token for which to retrieve the asset |
| assetId | uint64 | ID of the asset of which we are retrieving |

#### Returns

| Name | Type | Description |
|---|---|---|
| metadataURI | string | The metadata URI of the asset |
| equippableGroupId | uint64 | ID of the equippable group this asset belongs to |
| catalogAddress | address | The address of the catalog the part belongs to |
| partIds | uint64[] | An array of IDs of parts included in the asset |

### getAssetMetadata

```solidity
function getAssetMetadata(uint256 tokenId, uint64 assetId) external view returns (string)
```

Used to fetch the asset metadata of the specified token&#39;s active asset with the given index.

*Assets are stored by reference mapping `_assets[assetId]`.Can be overriden to implement enumerate, fallback or other custom logic.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId | uint256 | ID of the token from which to retrieve the asset metadata |
| assetId | uint64 | Asset Id, must be in the active assets array |

#### Returns

| Name | Type | Description |
|---|---|---|
| _0 | string | The metadata of the asset belonging to the specified index in the token&#39;s active assets  array |

### getAssetReplacements

```solidity
function getAssetReplacements(uint256 tokenId, uint64 newAssetId) external view returns (uint64)
```

Used to retrieve the asset that will be replaced if a given asset from the token&#39;s pending array  is accepted.

*Asset data is stored by reference, in order to access the data corresponding to the ID, call  `getAssetMetadata(tokenId, assetId)`.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId | uint256 | ID of the token to check |
| newAssetId | uint64 | ID of the pending asset which will be accepted |

#### Returns

| Name | Type | Description |
|---|---|---|
| _0 | uint64 | ID of the asset which will be replaced |

### getEquipment

```solidity
function getEquipment(uint256 tokenId, address targetCatalogAddress, uint64 slotPartId) external view returns (struct IERC6220.Equipment)
```

Used to get the Equipment object equipped into the specified slot of the desired token.

*The `Equipment` struct consists of the following data:  [      assetId,      childAssetId,      childId,      childEquippableAddress  ]*

#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId | uint256 | ID of the token for which we are retrieving the equipped object |
| targetCatalogAddress | address | Address of the `Catalog` associated with the `Slot` part of the token |
| slotPartId | uint64 | ID of the `Slot` part that we are checking for equipped objects |

#### Returns

| Name | Type | Description |
|---|---|---|
| _0 | IERC6220.Equipment | The `Equipment` struct containing data about the equipped object |

### getNestableAddress

```solidity
function getNestableAddress() external view returns (address)
```

Returns the Equippable contract&#39;s corresponding nestable address.




#### Returns

| Name | Type | Description |
|---|---|---|
| _0 | address | Address of the Nestable module of the external equip composite |

### getPendingAssets

```solidity
function getPendingAssets(uint256 tokenId) external view returns (uint64[])
```

Used to retrieve IDs of the pending assets of given token.

*Asset data is stored by reference, in order to access the data corresponding to the ID, call  `getAssetMetadata(tokenId, assetId)`.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId | uint256 | ID of the token to retrieve the IDs of the pending assets |

#### Returns

| Name | Type | Description |
|---|---|---|
| _0 | uint64[] | An array of pending asset IDs of the given token |

### isApprovedForAllForAssets

```solidity
function isApprovedForAllForAssets(address owner, address operator) external view returns (bool)
```

Used to check whether the address has been granted the operator role by a given address or not.

*See {setApprovalForAllForAssets}.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| owner | address | Address of the account that we are checking for whether it has granted the operator role |
| operator | address | Address of the account that we are checking whether it has the operator role or not |

#### Returns

| Name | Type | Description |
|---|---|---|
| _0 | bool | A boolean value indicating wehter the account we are checking has been granted the operator role |

### isChildEquipped

```solidity
function isChildEquipped(uint256 tokenId, address childAddress, uint256 childId) external view returns (bool)
```

Used to check whether the token has a given child equipped.

*This is used to prevent from transferring a child that is equipped.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId | uint256 | ID of the parent token for which we are querying for |
| childAddress | address | Address of the child token&#39;s smart contract |
| childId | uint256 | ID of the child token |

#### Returns

| Name | Type | Description |
|---|---|---|
| _0 | bool | A boolean value indicating whether the child token is equipped into the given token or not |

### rejectAllAssets

```solidity
function rejectAllAssets(uint256 tokenId, uint256 maxRejections) external nonpayable
```

Rejects all assets from the pending array of a given token.

*Effecitvely deletes the pending array.Requirements:  - The caller must own the token or be approved to manage the token&#39;s assets  - `tokenId` must exist.Emits a {AssetRejected} event with assetId = 0.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId | uint256 | ID of the token of which to clear the pending array. |
| maxRejections | uint256 | Maximum number of expected assets to reject, used to prevent from rejecting assets which  arrive just before this operation. |

### rejectAsset

```solidity
function rejectAsset(uint256 tokenId, uint256 index, uint64 assetId) external nonpayable
```

Rejects an asset from the pending array of given token.

*Removes the asset from the token&#39;s pending asset array.Requirements:  - The caller must own the token or be approved to manage the token&#39;s assets  - `tokenId` must exist.  - `index` must be in range of the length of the pending asset array.Emits a {AssetRejected} event.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId | uint256 | ID of the token that the asset is being rejected from |
| index | uint256 | Index of the asset in the pending array to be rejected |
| assetId | uint64 | ID of the asset expected to be in the index |

### setApprovalForAllForAssets

```solidity
function setApprovalForAllForAssets(address operator, bool approved) external nonpayable
```

Used to add or remove an operator of assets for the caller.

*Operators can call {acceptAsset}, {rejectAsset}, {rejectAllAssets} or {setPriority} for any token  owned by the caller.Requirements:  - The `operator` cannot be the caller.Emits an {ApprovalForAllForAssets} event.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| operator | address | Address of the account to which the operator role is granted or revoked from |
| approved | bool | The boolean value indicating whether the operator role is being granted (`true`) or revoked  (`false`) |

### setPriority

```solidity
function setPriority(uint256 tokenId, uint64[] priorities) external nonpayable
```

Sets a new priority array for a given token.

*The priority array is a non-sequential list of `uint64`s, where the lowest value is considered highest  priority.Value `0` of a priority is a special case equivalent to unitialized.Requirements:  - The caller must own the token or be approved to manage the token&#39;s assets  - `tokenId` must exist.  - The length of `priorities` must be equal the length of the active assets array.Emits a {AssetPrioritySet} event.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId | uint256 | ID of the token to set the priorities for |
| priorities | uint64[] | An array of priorities of active assets. The succesion of items in the priorities array  matches that of the succesion of items in the active array |

### supportsInterface

```solidity
function supportsInterface(bytes4 interfaceId) external view returns (bool)
```



*Returns true if this contract implements the interface defined by `interfaceId`. See the corresponding https://eips.ethereum.org/EIPS/eip-165#how-interfaces-are-identified[EIP section] to learn more about how these ids are created. This function call must use less than 30 000 gas.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| interfaceId | bytes4 | undefined |

#### Returns

| Name | Type | Description |
|---|---|---|
| _0 | bool | undefined |

### unequip

```solidity
function unequip(uint256 tokenId, uint64 assetId, uint64 slotPartId) external nonpayable
```

Used to unequip child from parent token.

*This can only be called by the owner of the token or by an account that has been granted permission to  manage the given token by the current owner.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId | uint256 | ID of the parent from which the child is being unequipped |
| assetId | uint64 | ID of the parent&#39;s asset that contains the `Slot` into which the child is equipped |
| slotPartId | uint64 | ID of the `Slot` from which to unequip the child |



## Events

### ApprovalForAllForAssets

```solidity
event ApprovalForAllForAssets(address indexed owner, address indexed operator, bool approved)
```

Used to notify listeners that owner has granted approval to the user to manage assets of all of their  tokens.



#### Parameters

| Name | Type | Description |
|---|---|---|
| owner `indexed` | address | Address of the account that has granted the approval for all assets on all of their tokens |
| operator `indexed` | address | Address of the account that has been granted the approval to manage the token&#39;s assets on all of  the tokens |
| approved  | bool | Boolean value signifying whether the permission has been granted (`true`) or revoked (`false`) |

### ApprovalForAssets

```solidity
event ApprovalForAssets(address indexed owner, address indexed approved, uint256 indexed tokenId)
```

Used to notify listeners that owner has granted an approval to the user to manage the assets of a  given token.

*Approvals must be cleared on transfer*

#### Parameters

| Name | Type | Description |
|---|---|---|
| owner `indexed` | address | Address of the account that has granted the approval for all token&#39;s assets |
| approved `indexed` | address | Address of the account that has been granted approval to manage the token&#39;s assets |
| tokenId `indexed` | uint256 | ID of the token on which the approval was granted |

### AssetAccepted

```solidity
event AssetAccepted(uint256 indexed tokenId, uint64 indexed assetId, uint64 indexed replacesId)
```

Used to notify listeners that an asset object at `assetId` is accepted by the token and migrated  from token&#39;s pending assets array to active assets array of the token.



#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId `indexed` | uint256 | ID of the token that had a new asset accepted |
| assetId `indexed` | uint64 | ID of the asset that was accepted |
| replacesId `indexed` | uint64 | ID of the asset that was replaced |

### AssetAddedToTokens

```solidity
event AssetAddedToTokens(uint256[] tokenIds, uint64 indexed assetId, uint64 indexed replacesId)
```

Used to notify listeners that an asset object at `assetId` is added to token&#39;s pending asset  array.



#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenIds  | uint256[] | An array of token IDs that received a new pending asset |
| assetId `indexed` | uint64 | ID of the asset that has been added to the token&#39;s pending assets array |
| replacesId `indexed` | uint64 | ID of the asset that would be replaced |

### AssetPrioritySet

```solidity
event AssetPrioritySet(uint256 indexed tokenId)
```

Used to notify listeners that token&#39;s prioritiy array is reordered.



#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId `indexed` | uint256 | ID of the token that had the asset priority array updated |

### AssetRejected

```solidity
event AssetRejected(uint256 indexed tokenId, uint64 indexed assetId)
```

Used to notify listeners that an asset object at `assetId` is rejected from token and is dropped  from the pending assets array of the token.



#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId `indexed` | uint256 | ID of the token that had an asset rejected |
| assetId `indexed` | uint64 | ID of the asset that was rejected |

### AssetSet

```solidity
event AssetSet(uint64 indexed assetId)
```

Used to notify listeners that an asset object is initialized at `assetId`.



#### Parameters

| Name | Type | Description |
|---|---|---|
| assetId `indexed` | uint64 | ID of the asset that was initialized |

### ChildAssetEquipped

```solidity
event ChildAssetEquipped(uint256 indexed tokenId, uint64 indexed assetId, uint64 indexed slotPartId, uint256 childId, address childAddress, uint64 childAssetId)
```

Used to notify listeners that a child&#39;s asset has been equipped into one of its parent assets.



#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId `indexed` | uint256 | ID of the token that had an asset equipped |
| assetId `indexed` | uint64 | ID of the asset associated with the token we are equipping into |
| slotPartId `indexed` | uint64 | ID of the slot we are using to equip |
| childId  | uint256 | ID of the child token we are equipping into the slot |
| childAddress  | address | Address of the child token&#39;s collection |
| childAssetId  | uint64 | ID of the asset associated with the token we are equipping |

### ChildAssetUnequipped

```solidity
event ChildAssetUnequipped(uint256 indexed tokenId, uint64 indexed assetId, uint64 indexed slotPartId, uint256 childId, address childAddress, uint64 childAssetId)
```

Used to notify listeners that a child&#39;s asset has been unequipped from one of its parent assets.



#### Parameters

| Name | Type | Description |
|---|---|---|
| tokenId `indexed` | uint256 | ID of the token that had an asset unequipped |
| assetId `indexed` | uint64 | ID of the asset associated with the token we are unequipping out of |
| slotPartId `indexed` | uint64 | ID of the slot we are unequipping from |
| childId  | uint256 | ID of the token being unequipped |
| childAddress  | address | Address of the collection that a token that is being unequipped belongs to |
| childAssetId  | uint64 | ID of the asset associated with the token we are unequipping |

### NestableAddressSet

```solidity
event NestableAddressSet(address old, address new_)
```

Used to notify listeners of a new `Nestable` associated  smart contract address being set.

*When initially setting the `Nestable` smart contract address, the `old` value should equal `0x0` address.*

#### Parameters

| Name | Type | Description |
|---|---|---|
| old  | address | Previous `Nestable` smart contract address |
| new_  | address | New `Nestable` smart contract address |

### ValidParentEquippableGroupIdSet

```solidity
event ValidParentEquippableGroupIdSet(uint64 indexed equippableGroupId, uint64 indexed slotPartId, address parentAddress)
```

Used to notify listeners that the assets belonging to a `equippableGroupId` have been marked as  equippable into a given slot and parent



#### Parameters

| Name | Type | Description |
|---|---|---|
| equippableGroupId `indexed` | uint64 | ID of the equippable group being marked as equippable into the slot associated with  `slotPartId` of the `parentAddress` collection |
| slotPartId `indexed` | uint64 | ID of the slot part of the catalog into which the parts belonging to the equippable group  associated with `equippableGroupId` can be equipped |
| parentAddress  | address | Address of the collection into which the parts belonging to `equippableGroupId` can be  equipped |



