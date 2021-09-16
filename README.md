# test
parameter(im0=500,jm0=200,ny=3)
real,dimension(im0,jm0)::x,y
real,dimension(im0,jm0,ny)::z,zn

open(1,file='1.txt')
open(11,file='2.txt')

read(1,*)im,jm
do i=1,im
 do j=1,jm
   read(1,*)ii,jj,x(i,j),y(i,j),(z(i,j,k),k=1,ny)
  enddo
enddo
zn=z
do i=1,im
  do j=1,jm
    zmax=-100
	do k=1,ny
	  if(zmax<=z(i,j,k)) zmax=z(i,j,k)
	enddo
	if(zmax>=35.)then
	 do k=1,ny
	  zn(i,j,k)=zmax
	 enddo
	endif
   enddo
 enddo

 write(11,100)im,jm
 do i=1,im
   do j=1,jm
	write(11,100)i,j,x(i,j),y(i,j),(zn(i,j,k),k=1,ny)
   enddo
 enddo

 100 format(2(i3,2x),2(f8.1,2x),3(f6.2,2x))
 stop
 end
