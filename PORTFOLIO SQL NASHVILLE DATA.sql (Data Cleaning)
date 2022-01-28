-- Date Cleaning in SQL

select * from PortfolioProject..Nashville

--Standardising Date Format

select SaleDate, convert(date, SaleDate)
from PortfolioProject..Nashville

update PortfolioProject..Nashville
set SaleDate= convert(date, SaleDate)

--Above did not work so alternate method:

alter table PortfolioProject..Nashville
add SaleDate2 date;

update portfolioproject..Nashville
set SaleDate2 = convert(date,SaleDate)

select SaleDate2
from PortfolioProject..Nashville


--Populate Property Address Data
--Ensuring that records with the same ParcelID have the same Property Address

select pn1.ParcelID, pn1.PropertyAddress, pn2.ParcelID, pn2.PropertyAddress, ISNULL(pn1.PropertyAddress, pn2.PropertyAddress)
from PortfolioProject..Nashville pn1
join PortfolioProject..Nashville pn2
on pn1.ParcelID= pn2.ParcelID and pn1.[UniqueID ]<> pn2.[UniqueID ]
where pn1.PropertyAddress is null

update pn1
set PropertyAddress = ISNULL(pn1.PropertyAddress, pn2.PropertyAddress)
from PortfolioProject..Nashville pn1
join PortfolioProject..Nashville pn2
on pn1.ParcelID= pn2.ParcelID and pn1.[UniqueID ]<> pn2.[UniqueID ]
where pn1.PropertyAddress is null


--Breaking out PropertyAddress into Address, City (Using SubStrings)

--Address

select SUBSTRING(PropertyAddress, 1, CHARINDEX(',', PropertyAddress)-1) as Address,
--City
SUBSTRING(PropertyAddress, CHARINDEX(',', PropertyAddress)+1, LEN(PropertyAddress)) as City
from PortfolioProject..Nashville

--Making new columns for Address and City

alter table PortfolioProject..Nashville
add PropertySplitAddress nvarchar(255);

update PortfolioProject..Nashville
set PropertySplitAddress = SUBSTRING(PropertyAddress, 1, CHARINDEX(',', PropertyAddress)-1)

alter table PortfolioProject..Nashville
add PropertySplitCity nvarchar(255);

update PortfolioProject..Nashville
set PropertySplitCity = SUBSTRING(PropertyAddress, CHARINDEX(',', PropertyAddress)+1, LEN(PropertyAddress))

--Breaking out OwnerAddress into Address, City, State (Using Parsename)

select PARSENAME(REPLACE(OwnerAddress,',','.'),3) as Address,
PARSENAME(REPLACE(OwnerAddress,',','.'),2) as City,
PARSENAME(REPLACE(OwnerAddress,',','.'),1) as State
from PortfolioProject..Nashville

alter table PortfolioProject..Nashville
add OwnerSplitAddress nvarchar(255)

update PortfolioProject..Nashville
set OwnerSplitAddress = PARSENAME(REPLACE(OwnerAddress,',','.'),3)

alter table PortfolioProject..Nashville
add OwnerSplitCity nvarchar(255)

update PortfolioProject..Nashville
set OwnerSplitCity = PARSENAME(REPLACE(OwnerAddress,',','.'),2)

alter table PortfolioProject..Nashville
add OwnerSplitState nvarchar(255)

update PortfolioProject..Nashville
set OwnerSplitState = PARSENAME(REPLACE(OwnerAddress,',','.'),1) 

--Change Y and N to Yes and No in "SoldasVacant" field
select SoldAsVacant, 
	case 
		when SoldAsVacant = 'Y' then 'Yes'
		when SoldAsVacant = 'N' then 'No'
	end
from PortfolioProject..Nashville

update PortfolioProject..Nashville
set SoldAsVacant = case when SoldAsVacant = 'Y' then 'Yes'
					when SoldAsVacant = 'N' then 'No'
					else SoldAsVacant
					end

-- Delete Duplicates (Upcoming)
-- Delete Unused Columns

alter table portfolioproject..Nashville
drop column OwnerAddress, TaxDistrict, PropertyAddress

alter table portfolioproject..Nashville
drop column SaleDate
