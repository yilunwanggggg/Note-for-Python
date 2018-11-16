# This is the notebook for Casjob

content



- The skill of SQL code
- The description of database


## 继续用casjob联合数据

主要是使用了sql的select distinct

SELECT DISTINCT
  m.cntr as cntr1,n.wise_cntr as cntr2,
  k.objID as objid1, n.objid as objid2,
  n.ra1,n.dec1,
  k.psfMag_u,k.psfMag_g,k.psfMag_r,k.psfMag_i,k.psfMag_z,
  m.w1mpro,m.w2mpro,m.w1mag_1,
  m.w2mag_1,m.w1mag_3,m.w2mag_3,
  m.j_m_2mass,m.k_m_2mass,m.h_m_2mass
from wise_2mass_data00 as m
  inner join wise_name00 as n
  on m.cntr = n.wise_cntr
  inner join wise_sdss_data00 as k
  on k.objID = n.objid
  into mydb.photo_sdss_wise_2mass00


## 最后还是用casjob

for wise:

get wise\_2mass\_data

select
  n.objid,m.cntr,m.w1mpro,m.w2mpro,m.w1mag_1,
  m.w2mag_1,m.w1mag_3,m.w2mag_3,
  m.j_m_2mass,m.k_m_2mass,m.h_m_2mass
from sdss_dr14.wise_allsky as m
into mydb.wise_2mass_data00
  inner join wise_name00 as n
  on m.cntr = n.wise_cntr
where m.w1mpro<17 and (m.w1snr > 2 and m.w2snr > 2)
  and m.j_m_2mass is not null
  and m.j_m_2mass < 9999

get wise\_sdss\_data:

select
  m.objID,n.cntr,
  m.psfMag_u,m.psfMag_g,m.psfMag_r,m.psfMag_i,m.psfMag_z
from sdss_dr14.photoobjall as m
into mydb.wise_sdss_data00
  inner join wise_2mass_data00 as n
  on m.objid = n.objid



select top 1000
  m.cntr,m.w1mpro,m.w2mpro,m.w1mag_1,
  m.w2mag_1,m.w1mag_3,m.w2mag_3,
  m.j_m_2mass,m.k_m_2mass,m.h_m_2mass
from sdss_dr14.wise_allsky as m
  inner join wise_nametest as n
  on m.cntr = n.wise_cntr
where m.w1mpro<17 and (m.w1snr > 2 and m.w2snr > 2)
  and m.j_m_2mass is not null

## ALLWISE
具体解释回头写


SELECT TOP 100
  n.objid, o.wise_cntr,n.distance,
  m.ra AS ra1, m.dec AS dec1
   from MyDB.for_wiseallsky0 AS m 
     OUTER APPLY dbo.fGetNearestObjEq( m.ra, m.dec, 1) AS n
     LEFT JOIN wise_xmatch AS o ON o.sdss_objid=n.objid
     where n.objid is not null and o.wise_cntr is not null

SELECT top 100
  designation,ra,dec,w1mpro,w2mpro,w1snr,w2snr,
  w1mag_1,w1mag_3,w2mag_1,w2mag_3,
  j_m_2mass,h_m_2mass,k_m_2mass
FROM ALLWISE.catalog
WHERE w1mpro<17 and (w1snr > 2 and w2snr >2)
  and j_m_2mass is not null
into mydb.allwise_2mass

目前来看，allwise 的数据库里可以可以直接得到2mass的数据，
这很好，然后对于非null数据，sql语言要求必须使用is not null来表示。


## SDSS:
DR14:

table specobjall:

>This is a base table containing ALL the spectroscopic information, including a lot of duplicate and bad data. Use the SpecObj view instead, which has the data properly filtered for cleanliness. These tables contain both the BOSS and SDSS spectrograph data. NOTE: The RA and Dec in this table refer to the DR8 coordinates, which have errors in the region north of 41 deg in Dec. This change does not affect the matching to the photometric catalog.

>**class**   varchar 32          Spectroscopic class (GALAXY, QSO, or STAR)

table photoobjall

>This table contains one entry per detection, with the associated photometric parameters measured by PHOTO, and astrometrically and photometrically calibrated.
The table has the following views:

>PhotoObj: all primary and secondary objects; essentially this is the view you should use unless you want a specific type of object.
PhotoPrimary: all photo objects that are primary (the best version of the object).
Star: Primary objects that are classified as stars.
Galaxy: Primary objects that are classified as galaxies.
Sky:Primary objects which are sky samples.
Unknown:Primary objects which are no0ne of the above
PhotoSecondary: all photo objects that are secondary (secondary detections)
PhotoFamily: all photo objects which are neither primary nor secondary (blended)

总之，目前联合两个表就这样：
关于所谓collate，就是各个国家的各个表可能是按照不同的格式写入的text。。。。。
反正我在这里心态崩了

'''
select obsid,ra,dec,class COLLATE SQL_Latin1_General_CP1_CI_AS from Lamost_dr3.catalogue
union all
select specobjid,ra,dec,class from SDSS_DR14.specObjall
into mydb.SDSS_LAMOST2
'''